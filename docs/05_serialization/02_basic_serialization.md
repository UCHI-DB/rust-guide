# String and Byte Serialization

## Byte Serialization

Basic File-IO operations are similar to those in other low-level languages
like C or C++. The following code sample demonstrates how to read and write
4 bytes (the typical size of a `u32` integer) to a file in Rust. 

```rust
fn write_bytes_to_file(bytes: [u8; 4], filename: &str) -> Result<(), Error> {
    // Create a File; see Rust doc for std::fs::File
    let mut buffer = File::create(filename)?;
    // Write bytes to that file
    buffer.write_all(&bytes)?;
    Ok(())
}

fn read_bytes_from_file(filename: &str) -> [u8; 4] {
    let f = File::open(filename).expect("could not open file");
    let mut reader = BufReader::new(f);
    let mut buffer = Vec::new();

    // Read file into vector.
    reader.read_to_end(&mut buffer).expect("error while reading file");

    // Transform Vec (much preferred way of handling collection of values) into array (for this example)
    let array = vec_to_array(buffer);
    array
}

fn vec_to_array<T, const N: usize>(v: Vec<T>) -> [T; N] {
    v.try_into()
        .unwrap_or_else(|v: Vec<T>| panic!("Expected a Vec of length {} but it was {}", N, v.len()))
}
```

The crux of serializing a data structure is to find a byte representation of the same. Different computer architectures, however, will interpret bits within a byte differently. 

In particular, when serializing numbers, byte order matters. Recall the differences between *Little* and *Big* Endian representation - you can read more in [the Wikipedia article on Endianness](https://en.wikipedia.org/wiki/Endianness). Rust provides multiple byte conversion traits for numeric types, such as `to_le_bytes` and `to_be_bytes` for little and big endian, respectively. The corresponding `from_le_bytes` and `from_be_bytes` are used to convert bytes back to numbers.


## String Serialization

The following code sample demonstrates how to read and write a string to a file in Rust. Like before, all values are first serialized to bytes and then read or written to a file.

```rust
fn write_string_to_file(string: &str, filename: &str) {
    let f = File::create(filename).expect("error creating file");
    let mut f = BufWriter::new(f);
    f.write_all(string.as_bytes()).unwrap();
}

fn read_string_from_file(filename: &str) -> String {
    let mut data = String::new();
    let f = File::open(filename).expect("error while opening file");
    let mut br = BufReader::new(f);
    br.read_to_string(&mut data).unwrap();
    data
}
```

Similarly, most variables can be serialized to a string representation using the `from_string()` and `to_string()` methods for numeric types.

