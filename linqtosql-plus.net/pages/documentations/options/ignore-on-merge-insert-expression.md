# IgnoreOnMergeUpdateExpression

## Description

Gets or sets columns to ignore when the `BulkMerge` method executes the `insert` statement.


```csharp
context.BulkMerge(list, options => 
        options.IgnoreOnMergeUpdateExpression = entity => new {entity.ModifiedDate, entity.ModifiedUser}
); 
```

## Purpose
The `IgnoreOnMergeInsertExpression` option lets you ignore some columns that should only be `updated.

By example, when to `update` the ModifiedData and ModifiedUser but not `insert` value.

## Limitations
Database Provider Supported:
- SQL Server
- SQL Azure

_Ask our support team if you need this option for another provider_
