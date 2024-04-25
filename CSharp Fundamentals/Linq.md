### What is LINQ?
Language Integrated Query or LINQ is the collection of standard query operators which provides query facilities into .NET languages like C# and VB.NET. Linq bridges the gap between the world of data and the world of objects. It enables querying against sources like arrays, enumerables, XMLs, relational databases and 3rd party data sources.

### What are the different types of LINQ?
LINQ to Objects, LINQ to SQL and LINQ to XML.

### What is the role of the `IEnumerable` interface?
`IEnumerable` is crucial in LINQ as it provides the foundation for iterating over a collection that LINQ queries against. Every query returns an `IEnumerable` or `IQueryable`, allowing further querying and collection manipulation.

### What is deferred execution?
Deferred execution means that the evaluation of an expression is delayed until its realized value is actually iterated over or called upon. This can be efficient in terms of memory or performance, but it can also result in unexpected behavior if used carelessly. E.g. you manipulate a list that you queried against but haven't converted back to a list with a `ToList()`.

### What is immediate execution?
Immediate execution occurs when the LINQ query is executed at the point of it's declaration, usually forced by calling methods like `ToList()`, `ToArray()`, or `Count()`.

### Explain lambda expressions and how they're used in LINQ.
A lambda expression is an ***anonymous function*** used to create ***delegates*** or ***expression tree*** types. In LINQ, they are often used to write inline expressions defining ***criteria*** or ***projections***.

### What are expression trees?
Expression trees represent code in a tree-like data structure, where each node is an expression, such as a method call or a binary operation. LINQ uses expression trees to translate queries against data sources like SQL into domain-specific language.

### What is the difference between `FirstOrDefault()` and `SingleOrDefault()`?
Both methods return a single element from a sequence. `FirstOrDefault()` returns the first found element or default if no element is found. `SingleOrDefault()` ***throws if there is more than one element*** in the sequence, otherwise, it returns the single element or default.

### Explain the purpose of the `Select` clause in LINQ.
The `Select` clause is used for ***projection***. It specifies the data elements that are retrieved from the data source.

### What does the `Where` clause do in a LINQ query?
The `Where` clause is used to ***filter*** records. It specifies which elements to include based on a boolean condition.

### How do you sort data in a LINQ query?
The `OrderBy` or `OrderByDescending` methods are used to sort data.

### What is LINQ to SQL?
**Answer:** LINQ to SQL is a component of .NET Framework which provides a run-time infrastructure for managing relational data as objects without losing the ability to query.

### What are extension methods?
Extension methods allow adding new methods to existing types without modifying the original type. Many LINQ methods are implemented as extension methods applying to the `IEnumerable` and `IQueryable` types.

### How does `GroupBy` work in LINQ?
**Answer:** `GroupBy` groups elements that share a common attribute. Each group is represented as a collection of objects and a key.

### Describe the difference between `Take()` and `Skip()` methods in LINQ.
`Take()` fetches the ***first N elements*** from a collection, while `Skip()` ***bypasses*** the first N elements and ***returns the rest***.

### Explain how `Join` works in LINQ.
`Join` correlates the elements of two collections based on matching keys. The result is a flat sequence of matched pairs from both collections.

### What is method syntax and query syntax in LINQ?
**Answer:** Method syntax (also known as fluent) uses extension methods included in the `System.Linq` namespace, while query syntax is more like SQL and uses query expressions.



