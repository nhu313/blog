blog
====
Whenever I try to learn a new language, I usually do the Roman Numeral kata in that language. The main point here is to focus on learning the syntax. The Roman Numeral kata doesn't cover everything, but it has loop, array, string, enough to a feel of the language. 

I will make the assumption that you already know how to code so I won't go into a lot of details. This is more of a....how do I translate Ruby code into Elixir. Elixir is a functional language. The way you approach a problem with Elixir is probably different than the way you do in Ruby, an object orientented language. But the point of this post is to get you familiar with Elixir syntax. 

Note:
When I say run, it means I ran the command in the terminal. It's often depicted with `$`.
When I edit a file, I will specify which file on the first line with a comment, e.g. `#test/roman_numeral_test.exs`. This means in the `test` directory, I edited the `roman_numeral_test.exs` file.

Create a new project call roman_numeral
```bash
$ mix new roman_numeral
```

Navigate into that project
```bash
$ cd roman_numeral
```

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
#test/roman_numeral_test.exs
defmodule RomanNumeralTest do
  use ExUnit.Case

  test "the truth" do
    assert 1 + 1 == 2
  end
end
```
The syntax here is straight forward. Elixir uses `defmodule` to group functions together. Think of the Math (http://www.ruby-doc.org/core-2.1.2/Math.html) module in Ruby. Here is the syntax on how to create a module.
```elixir
defmodule ModuleName do

end
```
In the next line, we `use ExUnit.Case` \\TODO ADD DESCRIPTION

Let's delete the generate test and create our first tes. 

```elixir
#test/roman_numeral_test.exs
  test "converts 0" do
    assert RomanNumeral.converts(0) == ""
  end
```
In this test I say, I called the function `converts` from the RomanNumeral module. I expect it to equal to an empty String "". When you run the test in the command line, you should get this error.

```bash
$ mix test

1) test converts 0 (RomanNumeralTest)
     test/roman_numeral_test.exs:4
     ** (UndefinedFunctionError) undefined function: RomanNumeral.converts/1
     stacktrace:
       (roman_numeral) RomanNumeral.converts(1)
       test/roman_numeral_test.exs:5
```
The error states that the test "converts 0" failed in the file `test/roman_numeral_test.exs` on line 4. The failure is that it can't find the function converts in the module RomanNumeral with 1 params (`RomanNumeral.converts/1`). 

Let's fix that by opening the `lib/roman_numeral.ex` and add this in.

```elixir
#lib/roman_numeral.ex
defmodule RomanNumeral do

  def converts(num) do

  end
end
```

Now when you run the test, you should get this error.
```bash
$ mix test
lib/roman_numeral.ex:3: warning: variable num is unused
Compiled lib/roman_numeral.ex
Generated roman_numeral.app

  1) test converts 0 (RomanNumeralTest)
     test/roman_numeral_test.exs:4
     Assertion with == failed
     code: RomanNumeral.converts(0) == ""
     lhs:  nil
     rhs:  ""
     stacktrace:
       test/roman_numeral_test.exs:5

Finished in 0.03 seconds (0.03s on load, 0.00s on tests)
1 tests, 1 failures

```
The only thing that you should be confused about is `lhs` and `rhs`. `lhs` stands for left hand side. `rhs` stands for right hand side. The error states that the assertion fail because the left hand side didn't equal to the right hand side. Remember that I didn't specify anything in the converts method, so by default it returns nil (also known as null in some languages). 

Let's make the test passed by making the function returns "".
```elixir
#lib/roman_numeral.ex
  def converts(num) do
    ""
  end
```
Now run `mix test` to make sure everything passes. 

Let's add our second test. 

```elixir
#test/roman_numeral_test.exs
  test "converts 1" do
    assert RomanNumeral.converts(1) == "I"
  end
```
