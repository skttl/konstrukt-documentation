---
description: Configuring searchable properties in Konstrukt, the back office UI builder for Umbraco.
---

# Searchable Properties

{% hint style="info" %}
**Work in Progress:** The documentation for this page is currently in progress.
{% endhint %}

## Defining searchable properties

#### **AddSearchableProperty(Lambda searchablePropertyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given property to the searchable properties collection. Property must be of type `String`. When set searches via the list view search and entity picker property editor search fields will search across the properties defined in this collection. If no properties are defined as searchable then these UI elements will be disabled.

````csharp
// Example
collectionConfig.AddSearchableProperty(p => p.FirstName);
````