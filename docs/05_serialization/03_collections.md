# Collections
### Part 2: The basics - Vector

Now let's move on to the `serde2_vector` crate, also included with this module. There is a function that creates a vector of an unknown size that is only known during execution. The contents of the vector are a monotonically increasing integer that starts in 0, so if the size is 5, then the vector will contain 0, 1, 2, 3, 4. After the vector is created, your goals are to:

* serialize the vector to bytes and write them to a file, as in `serde1` (to-submit)
* deserialize the vector from the bytes in the file and verify that the vector is correct, i.e., by verifying the numbers it contains are monotonically increasing (to-submit)

What is different in `serde2_vector`? What challenges did you find you did not in serde1? Think carefully about these questions. After you understand the answer, consider these others:

* Say you have to serialize 2 integers and one string, does serialization order matter? why?
* What if you have a collection of different variables, each with different a type. For example, a collection of objects that represent students, with attributes such as name, last name, birth date, description of interests, and more. How would you go about serializing and deserializing this data?

### Part 3: The basics - Hashmap

Now let's move to a more complicated data structure - hashmap. In `serde2_hashmap`, we create a hashmap with some unknown size. The key in the hashmap is a string and the value is an integer with type `i32`. Your tasks are to 

* serialize the hashmap to bytes and write them to a file, as in `serde1` (to-submit)

* deserialize the hashmap from the bytes in the file and verify that the hashmap is correct, i.e. you can run `cargo test` to verify if your program is correct. in main.rs, we provide a simple hashmap for you to debug. In `tests.rs`, a more random and complicated hashmap is created for test (to-submit)

What new challenges did you find compared to `serde2_vector`? 