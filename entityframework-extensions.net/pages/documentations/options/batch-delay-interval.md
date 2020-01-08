# BatchDelayInterval

## Definition

The batch delay interval is the delay between any two batch operations.

The `BatchDelayInterval` gets or sets a delay in milliseconds to wait between batches. The following example specifies the delay interval to 100 milliseconds between any two batch operations.

```csharp
context.BulkInsert(list, options => options.BatchDelayInterval = 100);
```

Try it: [EF Core](https://dotnetfiddle.net/lil9tq) | [EF6](https://dotnetfiddle.net/65v3k3)

You can also set batch size globally using `EntityFrameworkManager.BulkOperationBuilder`.

```csharp
// Global
EntityFrameworkManager.BulkOperationBuilder = builder => builder.BatchDelayInterval = 100;
```


**DO NOT** use this option with the transaction.

## Purpose
Having access to add a delay interval between batches may help to give responsivity to other applications by giving them a chance to insert data during the delay time.

## FAQ

### Why should I not use this option with a transaction?
You should not because it may often lead to lock and deadlock.

A transaction must be as short as possible and completed as soon as possible.
