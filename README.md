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
* Lambda expression - inline anonymous function. `=>` is the lambda operator
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

## LINQ methods
* Select()
* SelectMany()
* Any()
* Where()
* Skip()
* First
* FirstOrDefault
