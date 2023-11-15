# Getting Started

To run the code in this book, you'll need to be able to compile and run Gleam
code on your computer.

## Install Gleam

Follow [the instructions on
the official Gleam website](https://gleam.run/getting-started/installing/) for your specific
environment.

## Make a basic project

To run Gleam code, you need to be inside of a project. Run `gleam new whatever-you-want-to-put-here` in your shell and `cd` into the new directory it
has created. You'll know it worked if you see something along the lines of

```
Your Gleam project whatever-you-want-to-put-here has been successfully created.
```

## Run code with `gleam run`

Gleam will run the `main` function defined in
`src/whatever-you-want-to-put-here.gleam` (compiling the project if necessary
first) when you execute `gleam run` in your shell.

## Print to the shell with `io.debug`

You'll likely want to see the output of code you're writing. You can print any
value to stderr with `io.debug`:

```
import gleam/io

pub fn main() {
  io.debug("Hello world!")
}
```

<div class="warning">

Note that this **should only be used in development**. In an actual
application/library, you'll want to use functions like `io.println` to print to
stdout (which only take `String`s). See the [standard library documentation for
`gleam/io`](https://hexdocs.pm/gleam_stdlib/gleam/io.html) for more information.

</div>
