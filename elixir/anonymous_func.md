Anonymous function in Elixir is express as follow:
fn(arguments) -> body end

You can call the function like this:

```bash
iex> square = fn(x) -> x * x end
iex> square.(3)
9
```

Let's use this function with Enum.map, since it takes an anonymous function. 

```bash
iex> Enum.map([1, 3, 4], square)
[1, 9, 16]
```

A shorter way to write the anonymous function:

```bash
iex> Enum.map([1, 3, 4], &(&1 * &1))
[1, 9, 16]
```

Note that &1 is the first argument and if you have two argument, you use it as &2.  

You can also pass the reference to a function that's already declare. For example, if you have a Math module with the square function:

```elixir
defmodule Math do
  def square(a) do
    a * a
  end
end
```

You can pass it to Enum.map like this:

```bash
iex> Enum.map([1, 3, 4], &Math.square/1)
[1, 9, 16]
```

Note you need to specify the arity, which for us is 1, for Elixir to know which function you're referring to.
