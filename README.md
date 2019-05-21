# ChessL
The **C**ompact, **H**uman-**E**ditable, **S**imple **S**erialization
**L**anguage.

**ChessL** is a superset of JSON that's simple to understand, readable, and
easy to edit by hand.

# Why?

- [JSON]() is great, but it has a very low signal-to-noise ratio. It's
  uncomfortable to edit by hand, and to read.
- [YAML](), while human-friendly, is an unholy behemoth of a language. The
  specification is infamous for being more than ten times the size of the JSON
  spec, with many redundant or unnecessary features (including
  [9-63 ways of writing a multi-line string]).
- [TOML]() is nice for configuration files (which are basically a huge map of
  key:value pairs), but not as nice for heavily nested objects.
- [SDLang]() is great, but very uncomfortable to work with (as it's pretty much
  syntactic sugar for XML) and doesn't have a stable implementation in most
  sensible languages (Ruby, PHP, but not C? Come on).

There exists no serialization format I could find that makes it easy to
preserve definition order in associative arrays *and* to work with them.

In most JSON implementations, for example, you have two options for an
order-preserving associative array:

1. A list of pairs (makes it terrible to look up values by their key,
   which defeats the purpose of an associative array):

       {
           "order_preserving_map": [
               ["key1", "value1"],
               ["key2", "value2"]
           ]
       }
2. A normal object with a separate list of keys (makes it even worse to
   edit by hand):

       {
           "obj": {
               "key1": "value1",
               "key2": "value2"
           },
           "obj_keys": ["key1", "key2"]
       }

Neither of the two is acceptable for data meant to be edited by hand.

# Goals

1. Simple, unambigous grammar.

   One way of specifying multiline strings is fine. We don't need 63.

2. Human-readable and human-editable.

   YAML, while extremely easy to read, is easily one of the hardest
   config/serialization languages to edit. JSON has too low a
   signal-to-noise ratio. SDLang and TOML are excellent, but do not fit the
   other criteria.

3. Easy to work with in code.

   XML-style tree traversal is not easy to work with. JSON-style indexing
   is easy to work with. JSONPath and XPath are easy to work with.

4. Minimal.

   If in doubt, it's better to leave processing to the user than to the parser.
   We don't need a separate datetime type, since every program that needs to
   work with dates already has a datetime library that can parse strings.

5. Strict.

   The more errors a ChessL parser throws when trying to parse invalid ChessL,
   the better.

6. Associative arrays preserve order.

   This is an implementation detail, but any compliant implementation should
   preserve order in associative arrays, with an optional flag to disable
   this behavior.

7. Elements of associative arrays and lists can have attributes.

   This is a feature inspired by SDLang. While unconventional and somewhat
   weird to work with in many programming languages, I've found that it
   dramatically boosts the human-readability and human-editability of the
   language.

# License

Copyright (c) 2019 Slavfox

[![License: CC BY
4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

The contents of this repository are licensed under the
[Creative Commons Attribution 4.0 International]() license.


[JSON]: https://www.json.org/
[YAML]: https://yaml.org/
[9-63 ways of writing a multi-line string]: https://stackoverflow.com/questions/3790454/in-yaml-how-do-i-break-a-string-over-multiple-lines/21699210#21699210
[TOML]: https://github.com/toml-lang/toml
[SDLang]: https://sdlang.org/
[Creative Commons Attribution 4.0 International]: https://creativecommons.org/licenses/by/4.0/
