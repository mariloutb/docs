# AllowUpdatePrimaryKeys

## Description

Gets or sets if the key must also be included in columns to `UPDATE`.


```csharp
context.BulkMerge(list, options => options.AllowUpdatePrimaryKeys = true);
```

## Purpose
This option is rarely used. One scenario example is a custom key with a trigger that requires columns part of the key to also be `UPDATED`.
