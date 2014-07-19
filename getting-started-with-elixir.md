blog
====
I will make the assumption that you already know how to code so I won't go into a lot of details. This is more of a....how do I translate Ruby code into Elixir.

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
`mix.exs` contains your project information such as project name, version, and dependency. In Ruby world, it is the combination of your Gemfile + Gemspec. In Maven Java, it is your pom file.

Alright, let's start coding.


`mix test`

