---
description: Configuring a global filter in Konstrukt, the back office UI builder for Umbraco.
---

# Global Filters

{% hint style="info" %}
**Work in Progress:** The documentation for this page is currently in progress.
{% endhint %}

## Applying a global filter

Sometimes you may only want to work with a sub-set of data within a given table so this is where the `SetFilter` method comes in handy, allowing you to define a global filter to apply to all queries for the given collection.

#### **SetFilter(Lambda whereClauseExression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the filter where clause expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.SetFilter(p => p.Current);
````