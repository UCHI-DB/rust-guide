# Traits

A [trait](https://doc.rust-lang.org/book/ch10-02-traits.html) defines behavior (i.e., functions). This is similar to interfaces from other languages. You can associate behavior with types via Traits. When you do that, you are stating that those types implement the behavior defined by the Trait. Let's make all this concrete. Consider a trait called ```Summary```.

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

We can then associate this Trait with different types. When we do that, we also implement the functions, unlike above, where we only declare them. For example,

```rust
pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```

As you can see, we implemented the same trait, ```Summary```, on 2 different structs: NewsArticle, and Tweet. We are saying that although NewsArticle and
Tweet are two different types, they both implement the Summary behavior. In addition, NewsArticle and Tweet can implement other Traits and have a default implementation still (e.g. `impl Tweet`)