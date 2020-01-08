# LogDump

## Description

The `BulkOperation.LogDump` property which is of type `StringBuilder` log all the information related to database events when `UseLogDump` is enabled.

The following example assigns `LogDump` to local `StringBuilder` variable `logDump` when the `BulkOperationExecuted` event is executed. 

```csharp
StringBuilder logDump;

context.BulkSaveChanges(options =>
{
    options.UseLogDump = true;
    options.BulkOperationExecuted = bulkOperation =>
    {
        logDump = bulkOperation.LogDump;
    };
});
```

Try it: [EF Core](https://dotnetfiddle.net/1a5kbE) | [EF6](https://dotnetfiddle.net/v37ink)  

## Purpose
Getting database `log` can often be useful for debugging and see what has been executed under the hood by the library.
