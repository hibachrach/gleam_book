# What is Gleam?

Gleam is a programming language! Though you may already know that before reading
this. But my guess is you want to learn more. Well let's get to it. But before
diving in, it's worth asking...why learn Gleam? Let's try to make the case:

# Gleam is friendly

## The Language

We're several words in here talking about a programming language without showing
you what it looks like. Let's change that. Here's a simple Gleam program:

```gleam
import gleam/bytes_builder
import gleam/http/response
import gleam/erlang/process
import mist

pub fn main() {
  fn(_request) { say_hello() }
  |> mist.new
  |> mist.port(3000)
  |> mist.start_http

  process.sleep_forever()
}

fn say_hello() {
  response.new(200)
  |> response.set_header("content-type", "text/plain")
  |> response.set_body(body_from_string("Hello World!"))
}

fn body_from_string(str) {
  str
  |> bytes_builder.from_string
  |> mist.Bytes
}
```

This program starts up a web server that responds with "Hello World!" to any web
request. But you may have been able to figure that out even though you haven't
learned any Gleam yet. As you'll find, most functions, types, and constants are
labeled clearly in common whole words.

For the most part, programs are composed out of a small set of things:

- a few base data types you're probably already familiar with
- custom types (similar to "structs" or "records" in other languages)
- pure functions
- a pattern matching operator

That's it! Gleam does not have any of the following:

- mutable values
- inheritance
- interfaces
- function/method/operator overloading
- meta-programming
- hidden function calls
- exceptions
- early returns

As a result, Gleam code is remarkably accessible.

## The Compiler

If you make a mistake when writing a Gleam program, the compiler is there to
help. Consider the `main` function from above. Imagine if we accidentally wrote
the port as a string instead of a number like so:

```gleam
pub fn main() {
  fn(_req) { say_hello() }
  |> mist.new
  |> mist.port("3000") // This won't work!
  |> mist.start_http

  process.sleep_forever()
}
```

When I try to compile the program,
this is what the compiler tells me:

```
error: Type mismatch
  ┌─ /path/to/file.gleam:9:16
  │
9 │   |> mist.port("3000")
  │                ^^^^^^

Expected type:

    Int

Found type:

    String
```

# Gleam is expressive

# Gleam scales

# Gleam comes batteries-included
