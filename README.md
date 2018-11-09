# LINQ-lesson
###### lets learn LINQwerwer!

## I. What is LINQ?

LINQ is not a character from The Legend of Zelda video game series (thats Link!).

![linq](https://user-images.githubusercontent.com/26471447/43230462-8f3e7d7e-9025-11e8-9398-e7bbe0bf9681.png)

![screenshot_12](https://user-images.githubusercontent.com/26471447/43231660-8394048a-902a-11e8-8184-a9d2e2fe720b.png)

I learned about software development at [Turing]() where I gained the skills to build single page applications using modern JavaScript libraries. This looked great on job applications, and certainly helped me land my first job. However, it would be a number of months before I could put my knowledge of React and Webpack to use. The web application I was developing in was built on the ASP.NET framework, whose main language is C#. 

Learning a new programming language at the first job of your new career can be daunting. I felt lost but through mentorship and learning from my incredible team and hours spent on Pluralsight I felt like I could stay afloat. 

It wasn't until I felt confident in C# that I really took deep dive into LINQ - and that's when I learned I should have started studying LINQ far sooner than I did. 
sdfgsdfg
LINQ (Language Integrated Query) is a query syntax available in C# and Visual Basic that provides methods for `traversing`, `filtering` and `projecting` data from different sources (SQL, Entities, Objects, XML, Google, Ebay, Twitter). 

From someone whose experience was based in front end web development, I like to think of LINQ methods for C# collections like array prototype methods in JavaScript. 

## II. High-level LINQ
### Query syntax: declarative
* Query expression operates on one or more data sources by applying one or more query operators
* Not every LINQ operator is available using this syntax
* Resembles SQL query format
### Method syntax: imperative
* The enumerable class in C# contains LINQ operators as `extension methods`. `Extension methods` are similar to array prototypes in JavaScript.
* Delegate - a method parameter of type function that is a method signature (the `callback function` of a LINQ lambda expression)
* Lambda expression - inline anonymous function. 
  * `=>` is the lambda operator
  * Does not require a return statement, but multi-line statements require curly braces and a return statement
  * Lambda expressions are very similar to ECMAScript 6 arrow functions.
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
  * Can use `ToList()` to execute a LINQ query and return a list

## III. Deep LINQ
### Sorting
* `OrderBy()` can be followed by `ThenBy()` for advanced ordering via chaining methods together. Can use as many `ThenBy()` as necessary, but only one `OrderBy()`
### Creating
* `Range()` takes two parameters, starting value and ending value
  * Can use `Select()` on a range to `project` an arithmatic sequence
```
var intergers = Enumerable.Range(0, 10); // returns [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

var intergers = Enumerable.Range(0, 10).Select(i => (i - 2) + (i * 2)); // returns [-2, 1, 4, 7, 10, 13, 16, 19, 22, 25, 28]

var letters = Enumerable.Range(0, 10).Select(i => ((char)('A' + i).ToString()); // returns [A, B, C, D, E, F, G, H, I, J]
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

public class FootballTeam 
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
		FullName = "The" + f.Hometown + " " + f.Name
	});
```
* Use `Join()` operater any time you need to combine related data into one query and return a new type
```
Enumerable.Join(
	OuterList, // a collection ( Join() can be called on this list )
	InnerList, // a collection related to the OuterList
	OuterSelector, // Lambda expression of data to select (think Lambda of Select())
	InnerSelector, // Lambda expression of data to select (think Lambda of Select())
	ResultSelector // Final Lambda expression, project data from collections into new object or result
	)
```
### Parent/Child and Master/Detail
Use `SelectMany()` to flatten multiple collections into a single sequence
 
## IV. Crunching the numbers
Use `Sum()` on a specific property of an object to return the sum, and `Average()` to return the average value of a specific object property.

### Grouping / Summing
`GroupBy()` takes 3 parameters, the key selector (what we are grouping by), the element selector which defines the values to select from the list, and the results selector, which uses the first two selectors as parameters in the lambda function to return a new type. 

## V. Some (not all) LINQ methods
### Sort
* First(), Last()
  * Will return first/last element of collection, but throw exception when there are no results. 
* FirstOrDefault(), LastOrDefault()
  * Will return first/last element of collection, but return null if there is no result. 
* OrderBy(), OrderByDescending(), ThenBy(), ThenByDescending()
  * Sorting operators sorting in ascending or descending order
* Reverse()
  * Reverse the order of a sequence
* Skip()
  * Will skip element in collection
* Where()
  * Returns a filtered sequence based on conditional expression in the method delegate
* Any()
  * Returns true when any single element in a sequence satisfy a condition else returns false
* All()
  * Returns true when any all elements in a sequence satisfy a condition else returns false
### Create
* Range()
  * Create numbers in a range
* Repeat()
  * Return mutliple occurances of a given value
* Add()
  * Will add single element to a collection
* AddRange()
  * Will add a collection to a collection
### Compare/Combine
* Intersect()
  * Uses equality compare to return the intersection of two sequences
* Except()
  * Returns sequence that contains the set difference of the elements of two sequences
* Concat()
  * Concatentes two sequences
* Distinct()
  * Returns a sequence containing only unique elements
* Union()
  * Returns collection of unique elements between two sequences
### Transform/Project
* Select()
  * Transform each element by using lambda expression (think map array prototype in JavaScript)
* SelectMany()
  * Used when we have a sequence of objects which has a collection property and we need to enumerate each item of child collection one by one
* Join()
  * Join two sequences based on matching keys
### Total
* Sum()
  * Returns sum of all elements in a sequence 
### Group / Sum
*  GroupBy()
  * Group elements based on a specific key
### Mean, Median, Mode
* Average()
  * Returns average of all elements in a sequence
  
  ---

formatting for medium
V. Some (not all) LINQ methods
Sort Methods
First(), Last()
Will return the first or last element of collection respectively, but will throw an exception when there are no results.

FirstOrDefault(), LastOrDefault()
Will return first/last element of collection, but return null if there is no result.

OrderBy(), OrderByDescending(), ThenBy(), ThenByDescending()
Sorting operators sorting in ascending or descending order

Reverse()
Reverse the order of a sequence

Skip()
Will skip element in collection

Where()
Returns a filtered sequence based on conditional expression in the method delegate

Any()
Returns true when any single element in a sequence satisfy a condition else returns false

All()
Returns true when any all elements in a sequence satisfy a condition else returns false

Create Methods
Range()
Create numbers in a range

Repeat()
Return multiple occurrences of a given value

Add()
Will add single element to a collection

AddRange()
Will add a collection to a collection

Compare/Combine Methods
Intersect()
Uses equality compare to return the intersection of two sequences

Except()
Returns sequence that contains the set difference of the elements of two sequences

Concat()
Concatenates two sequences

Distinct()
Returns a sequence containing only unique elements

Union()
Returns collection of unique elements between two sequences

Transform/Project
Select()
Transform each element by using lambda expression (think map array prototype in JavaScript)

SelectMany()
Used when we have a sequence of objects which has a collection property and we need to enumerate each item of child collection one by one

Join()
Join two sequences based on matching keys

Total
Sum()
Returns sum of all elements in a sequence

Group / Sum
GroupBy()
Group elements based on a specific key

Mean, Median, Mode
Average()
Returns average of all elements in a sequence
