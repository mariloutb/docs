# ColumnInputExpression

## Description

Gets or sets columns to map with the direction `Input`.

The key is required for operations such as `BulkUpdate` and `BulkMerge`.


```csharp
context.BulkMerge(list, options => 
        options.ColumnInputExpression = entity => new {entity.ID, entity.Code}
); 
```

## Purpose
The `ColumnInputExpression` option lets you choose specific properties in which you want to perform the bulk operations.

By example, when importing a file, you may not have data on all properties.
