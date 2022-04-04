# C\#

## Resources

- [C# Programming Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/)
- [C# Reference](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/)
    - [Keywords](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/)
      (`new`, `this`, `public`, `private`, `null`, `case`, …)
    - [Iteration statements](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/statements/iteration-statements)
      (`for`, `foreach`, …)
    - Types
        - [Value types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types)
          (`bool`, `char`, `int`, `double`, [structure types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct), …)
        - [Reference types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types)
          (`class`, `interface`, …)
- [Collections and Data Structures](https://docs.microsoft.com/en-us/dotnet/standard/collections/)
  (`IEnumerable`, `IList`, `IDictionary`, …)
- Arrays
    - [Arrays Programming Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/)
    - [`System.Array`](https://docs.microsoft.com/en-us/dotnet/api/system.array)
- Strings
    - [Strings Programming Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/)
    - [`System.String`](https://docs.microsoft.com/en-us/dotnet/api/system.string)
- [LINQ Queries](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities#method-based-query-syntax)
- [Nullable Reference Types](https://docs.microsoft.com/en-us/dotnet/csharp/nullable-references)

## How Tos

- [C# How to Articles](https://docs.microsoft.com/en-us/dotnet/csharp/how-to/)
    - [Auto Properties](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties)
    - [Object and Collection Initializers](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers)
    - [Split Strings](https://docs.microsoft.com/en-us/dotnet/csharp/how-to/parse-strings-using-split)
    - [Concatenate Strings](https://docs.microsoft.com/en-us/dotnet/csharp/how-to/concatenate-multiple-strings)
    - [Search Strings](https://docs.microsoft.com/en-us/dotnet/csharp/how-to/search-strings)
    - [Compare Strings](https://docs.microsoft.com/en-us/dotnet/csharp/how-to/compare-strings)

## NUnit

- [`TestFixture`](https://docs.nunit.org/articles/nunit/writing-tests/attributes/testfixture.html)
- [`TestCase`](https://docs.nunit.org/articles/nunit/writing-tests/attributes/testcase.html)
- [`SetUp` and `TearDown`](https://docs.nunit.org/articles/nunit/writing-tests/setup-teardown/index.html)
- [Assertions](https://docs.nunit.org/articles/nunit/writing-tests/assertions/assertion-models/constraint.html)
  (`Assert.That(myOutput, Is.SomeConstraint)`)
- [Constraints](https://docs.nunit.org/articles/nunit/writing-tests/constraints/Constraints.html)
  (`Is.Empty`, `Is.EqualTo`, `Contains.Item`, …)

## Tools

- [.NET Fiddle](https://dotnetfiddle.net/) - write, run and share C# code in the browser

## Talks

- [What I've learned from 20 years of programming in C# with Joe Albahari](https://www.youtube.com/watch?v=_TMZsPjoGJA)
  - Types
    - [implicit conversion](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/user-defined-conversion-operators)
  - Functional Programming
    - Lazy values
    - Closures
  - Asynchronous Programming
  - Sum Types (experimental custom implementation)
