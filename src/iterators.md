# Iterators

Iterators are similar to lists, except they are lazily evaluated. This is useful
when a list would be unreasonable (or impossible) to represent in memory. For
example, here's how we could create an iterator for the Fibonacci numbers:

```gleam
import gleam/iterator

fn fibonacci() {
  iterator.unfold(
    from: #(0, 1),
    with: fn(prev_two) {
      let #(first, second) = prev_two
      iterator.Next(element: second, accumulator: #(second, first + second))
    },
  )
}

fn main() {
  fibonacci_iter()
  |> iterator.take(up_to: 10)
  |> iterator.to_list
  |> io.debug // => [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
}
```

Note that, like all data types in Gleam, iterators are immutable. Therefore, all
traversals, maps, etc. always start at the beginning each time:

```gleam
  let f = fibonacci_iter()

  f
  |> iterator.take(up_to: 10)
  |> iterator.to_list
  |> io.debug // => [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

  f
  |> iterator.take(up_to: 10)
  |> iterator.to_list
  |> io.debug // => [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

Of course, you can create new iterators from existing iterators by composing
these functions:

```gleam
  let f = fibonacci_iter()

  f
  |> iterator.drop(up_to: 5)
  |> iterator.take(up_to: 3)
  |> iterator.to_list
  |> io.debug // => [8, 13, 21]
```

See more ways to create and manipulate iterators [in the
docs](https://hexdocs.pm/gleam_stdlib/gleam/iterator.html).
