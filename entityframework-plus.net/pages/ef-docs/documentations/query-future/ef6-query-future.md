---
Permalink: query-future
---

# Query Future

## Description

Every time an immediate method like **ToList** or **FirstOrDefault** is invoked on a query, a database round trip is made to retrieve data. While most applications don't have performance issues with making multiple round trips, batching multiple queries into one can be critical for some heavy traffic applications for scalability. Major ORM like NHibernate had this feature for a long time but, unfortunately for Entity Framework users, batching queries is only available through third party libraries.

**EF+ Query Future** opens up all batching future queries features for Entity Framework users.

To batch multiple queries, simply append **Future** or **FutureValue** method to the query. All future queries will be stored in a pending list, and when the first future query requires a database round trip, all queries will be resolved in the same SQL command.

{% include template-example.html %} 
```csharp

// using Z.EntityFramework.Plus; // Don't forget to include this.
var ctx = new EntitiesContext();

// CREATE a pending list of future queries
var futureCountries = ctx.Countries.Where(x => x.IsActive).Future();
var futureStates = ctx.States.Where(x => x.IsActive).Future();

// TRIGGER all pending queries in one database round trip
// SELECT * FROM Country WHERE IsActive = true;
// SELECT * FROM State WHERE IsActive = true
var countries = futureCountries.ToList();

// futureStates is already resolved and contains the result
var states = futureStates.ToList();

```

[Try it](https://dotnetfiddle.net/NnXMtb)

## EF+ Query Future

Query Future delays the execution of a query returning an IEnumerable.

{% include template-example.html %} 
```csharp

// using Z.EntityFramework.Plus; // Don't forget to include this.
var ctx = new EntitiesContext();

// CREATE a pending list of future queries
var futureCountries = ctx.Countries.Where(x => x.IsActive).Future();
var futureStates = ctx.States.Where(x => x.IsActive).Future();

// TRIGGER all pending queries in one database round trip
// SELECT * FROM Country WHERE IsActive = true;
// SELECT * FROM State WHERE IsActive = true
var countries = futureCountries.ToList();

// futureStates is already resolved and contains the result
var states = futureStates.ToList();

```

[Try it](https://dotnetfiddle.net/NnXMtb)

## Options

 - [FutureValue](options/ef6-query-future-value.md)
 - [FutureValue Deferred](options/ef6-query-future-value-deferred.md)
 
## Real Life Scenarios

 - [Multi Tables Information](scenarios/ef6-query-future-multi-tables-information.md)
 - [Paging](scenarios/ef6-query-future-paging.md)

## Behind the code

 - All queries from a context using query future are added to a batch list.
 - When the first database round trip is required:
   - All sql commands are combined into one sql command.
   - The sql command is executed and a data reader is returned.
   - For every result in the data reader, the result is set to the corresponding query future.

## Limitations

 - Provider:
   - Provider not supported are added on demand
   - Provider which doesn't support multiple statements like SQL Compact cannot be supported

## Conclusion

As we saw, EF+ Query Future follows a good architecture principle:

 - **Flexible:** Future, FutureValue and FutureValue deferred make it possible to use it in any kind of scenario.
 - **Maintainable:** The easy to use API, documentation and available source code allows new developers to quickly understand this feature.
 - **Scalable:** Query Future only gets better as the number of user/traffic grows by drastically reducing database round trips.

Need help getting started? [info@zzzprojects.com](mailto:info@zzzprojects.com)

We welcome all comments, ideas and suggestions to improve our library.
