# linq-lesson
###### lets learn linq!

## I. Intro
* Like SQL queries
* C# (Visual Studio) and Visual Basic
* LINQ has providers for the following data sources: SQL, Entities, Objects, XML, Google, Ebay, Twitter

A query expression operates on one or more data sources by applying one or more query operators

## II. LINQ by example
* Query syntax: declarative
  * Query expression operates on one or more data sources by applying one or more query operators
* Method syntax: imperative

```
function find(customerList, customerId) {

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

	return customerList.Where(c.customerId == customerId);

}
```

* Linq uses `deferred execution` - linq query is defined, but not executed until the result is required
