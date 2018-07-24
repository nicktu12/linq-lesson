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
* To find the intersection of two sequences of numbers: 
```Enumerable.Intersect(seq1, seq2)```
or
```seq1.Intersect(seq2)```
* `Distinct()` only returns unique values
  * `Union()` can be used to combine lists and return only unique values
### Projections
Projection refers to transforming an object to a new form (think about `map` array prototype in JavaScript)
* Can project from a list of complex objects to a list of object properties
* Projections can be used to transform data into any shape you need
```
// Suppose we have a list of football teams, each represented by an object such as:

public class footballTeam 
{
	public string Name {get; set;}
	public string Hometown {get; set;}
	public string Mascot {get; set;}
	public List<Players> {get; set;}	
}

// We can generate (or project) a new list of team mascots using Select() on a list of teams

footballTeamList.Select(f => f.Mascot);

// Create a new anonymous type using new keyword

footballTeamList.Select(f => new 
	{
		Name = f.Name,
		Hometown = f.Hometown,
		FullName = "The" + f.Hometown + f.Name
	});
```
* Use `Join()` operater any time you need to combine related data into one query and return a new type
```
Enumberable.Join(
	OuterList, // a collection ( Join() can be called on this list )
	InnerList, // a collection related to the OuterList
	OuterSelector, // Lambda expression of data to select (think Lambda of Select())
	InnerSelector, // Lambda expression of data to select (think Lambda of Select())
	ResultSelector // Final Lambda expression, project data from collections into new object or result
	)
```
### Parent/Child and Master/Detail
Use `SelectMany()` to flatten multiple collections into a single collection
 
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
* Join()
### There's more!
* Any()
* Where()
