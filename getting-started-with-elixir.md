blog
====
Whenever I try to learn a new language, I usually do the Roman Numeral kata in that language. The main point here is to focus on learning the syntax. The Roman Numeral kata doesn't cover everything, but it has loop, array, string, enough to a feel of the language. 

I will make the assumption that you already know how to code so I won't go into a lot of details. This is more of a....how do I translate Ruby code into Elixir. Elixir is a functional language. The way you approach a problem with Elixir is probably different than the way you do in Ruby, an object orientented language. But the point of this post is to get you familiar with Elixir syntax. 

Note:
When I say run, it means I ran the command in the terminal. It's often depicted with `$`.
When I say run test, I mean in the command line, type `mix test`.
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

Rerun the test will give you a failure. I can make this pass by adding an if statement. http://elixir-lang.org/getting_started/5.html#toc_4

```elixir
#lib/roman_numeral.ex
  def converts(num) do
    if num < 1 do
      ""
    else
      "I"
    end
  end
```
We can also achieve the same result with a guard statement. 

```elixir
#lib/roman_numeral.ex
  def converts(num) when num < 1 do
    ""
  end

  def converts(num) do
    "I"
  end
```
Note that I created two methods which is similar to an if statement. The first method has `when num < 1 do` which is what we call a guard statement. It says call me if the number is less than 1, then I will return `""`. If that condition is not met, then it goes to the next function of the same name and parameters. It will continue to do so until it finds a function that matches. In this case, our next function is `def converts(num) do` which doesn't have a guard statement, therefore it "matches" so we get `"I"`.

Ok. If you run the test now, it should still pass. 

Let's add another test. 
```elixir
#lib/roman_numeral.ex
  test "converts 2" do
    assert RomanNumeral.converts(2) == "II"
  end
```
There are two ways to do this. One, we can multiply the number by the Roman numeral. 
```elixir
#lib/roman_numeral.ex
  def converts(num) do
    String.duplicate("I", num)
  end
```
Or you can do it through a loop. I will use a loop because the point of this exercise it to learn Elixir syntax. Remember Elixir is a functional language. So how can you loop without changing state of a variable? The answer is recursion!!! This is what the code should look like.  

```elixir
#lib/roman_numeral.ex
defmodule RomanNumeral do
  def converts(num) when num < 1 do
    ""
  end

  def converts(num) do
    "I" <> converts(num-1)
  end
end
```

You can probably figure out that `<>` is Elixir way to concatenate a String. For those of you who are still confused, let's walk through the code when the number is 2. When we call RomanNumeral.converts, it will try to find a method that matches that. `def converts(num) when num < 1 do` doesnt, but `def converts(num)` does. So it goes into this method `def converts(num) do`. It creates the String "I" and concatenate it to `converts(num-1)` which is really saying converts(1). Again, we know the first method doesn't match, so it goes into `def converts(num)` again. This time, remeber num is 1. So it again creates a "I" string, then calls converts again on num - 1 which is 0. Calling converts on 0 will return `""` because num is less than 1. Still confused? Think of it like this

2 -> 1 + 1 + 0 -> "I" <> "I" <> "" -> "II"

```elixir
#lib/roman_numeral.ex
defmodule RomanNumeral do
  def converts(num) when num < 1 do
    ""
  end

  def converts(num) do
    "I" <> converts(num-1)
  end
end
```

If you are still confuse, watch this video on recursion [\\TODO find video]
