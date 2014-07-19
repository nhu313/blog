blog
====
Whenever I try to learn a new language, I often do Roman Numeral kata in that language. Because I've done it so many time, I know how to solve it. Thus I can focus on learning the syntax. 

I will make the assumption that you already know how to code so I won't go into a lot of details. This is more of a....how do I translate Ruby code into Elixir. Elixir is a functional language. The way you approach a problem with Elixir is probably different than the way you do in Ruby, an object orientented language. But the point of this post is to get you familiar with Elixir syntax. 

Create a new project call roman_numeral
`mix new roman_numeral`

Navigate into that project
`cd roman_numeral`

This is the tree structure. 
```bash
├── README.md
├── config
│   └── config.exs
├── lib
│   └── roman_numeral.ex
├── mix.exs
└── test
    ├── roman_numeral_test.exs
    └── test_helper.exs
```
You can probably guess what they mean. 
`config` is for configuration. We won't touch this folder at all today.
`lib` is for your source code.
`test` is for your test code.
`mix.exs` contains your project information such as project name, version, and dependency. In Ruby world, it is the combination of your Gemfile + Gemspec. In Maven Java, it is your pom file. In clojure it is your project.clj.

Alright, let's start coding.
First, run the test.
`mix test`

You should see one passing test that mix created. Let's open the test file and see what that test looks like. 
```elixir 
defmodule RomanNumeralTest do
  use ExUnit.Case

  test "the truth" do
    assert 1 + 1 == 2
  end
end
```
The syntax here is pretty easy to understand. Elixir uses `defmodule` to group functions together, similar to a class in Ruby. But remember, Elixir is functional so you can't initiate the class to create an instance. Here is the syntax on how to create a module.
```elixir
defmodule ModuleName do

end
```
In the next line, we `use ExUnit.Case` 
