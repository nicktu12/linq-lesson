# linq-lesson
###### lets learn 

## I. Intro
* Like SQL queries
* C# (Visual Studio) and Visual Basic
* LINQ has providers for the following data sources: SQL, Entities, Objects, XML, Google, Ebay, Twitter
* Allows for `traversal`, `filtering` and `ojection` of collections

A query expression operates on one or more data sources by applying one or more query operators

## II. LINQ by example
### Query syntax: declarative
* Query expression operates on one or more data sources by applying one or more query operators
* Not every LINQ operator is available using thid syntax
### Method syntax: imperative
* Enumerable class contains LINQ operators as `extension methods`
* Delegate - a method parameter of type function that is a method signature, or the `callback function` of a LINQ lambda expression
* Lambda expression - inline anonymous function. 
  * `=>` is the lambda operator
  * Does not require a return statement, but multi-line statements require curly braces and a return statement
* Methods can be chained together in fluid programming style, meaning output of one method is input to the next

```
public Customer Find(List<Customer> customerList, int customerId) {

	// using for loop

	foreach (var c in customerList)
	{
		if (c.CustomerId == customerId)
		{
			return c;
		}
	}

	// using query syntax

	var query = 	from c in customerList
			where c.customerId == customerId
			select c;

	return query.First();

	// using method syntax

	return customerList.FirstOrDefault(c => c.customerId == customerId);

}
```

* LINQ uses `deferred execution` - LINQ query is defined, but not executed until the result is required

## III. more examples
### Sorting
* `OrderBy()` can be followed by `ThenBy()` for advanced ordering via chaining methods together. Can use as many `ThenBy()` as necessary, but only one `OrderBy()`
### Creating
* `Range()` takes two parameters, starting value and ending value
  * Can use `Select()` on a range to project an arithmatic sequence
```
var intergers = Enumerable.Range(0, 10); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

var intergers = Enumerable.Range(0, 10).Select(i => (i - 2) + (i * 2)); // -2, 1, 4, 7, 10, 13, 16, 19, 22, 25, 28

var letters = Enumerable.Range(0, 10).Select(i => ((char)('A' + i).ToString()); // A, B, C, D, E, F, G, H, I, J
```
### Compare/Combine

 
## Some LINQ methods
### Sort
* First()
* FirstOrDefault()
* Last()
* LastOrDefault()
* OrderBy()
* OrderByDescending()
* ThenBy()
* ThenByDescending()
* Reverse()
* Skip()
### Create
* Range()
* Repeat()
### Compare/Combine
* Intersect()
* Except()
* Concat()
* Distinct()
* Union()
### Transform/Project
* Select()
* SelectMany()
### There's more!
* Any()
* Where()
