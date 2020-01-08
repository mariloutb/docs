# ColumnOutputExpression

## Description

Gets or sets columns to map with the direction `Output`.


```csharp
context.BulkMerge(list, options => 
        options.ColumnOutputExpression = entity => new {entity.ModifiedDate, entity.ModifiedUser}
); 
```

## Purpose
The `ColumnOutputExpression` option lets you choose specific properties in which you want to retrieve data from the database.
