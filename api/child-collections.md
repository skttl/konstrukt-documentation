---
description: Configuring child collections in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Child Collections

A child collection is a container for a given data model that is tied to a parent collection data model. It shares all of the [Collections](collections.md) config builder API except child collections cannot contain other child collections.

By default, child collections will be made presented in the UI as context apps in the parent models editor view. If you have multiple child collections that make the context apps area over populated, you can use the [Child Collection Groups](child-collection-groups.md) to group child collections under a single context app with the inner child collections then being arranged in tabs.

## Defining a child collection

You define a child collection by calling one of the `AddChildCollection` methods on a given [`Collection`](collections.md) config builder instance.

#### AddChildCollection&lt;TChildEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, Lambda childCollectionConfig = null) : *KonstruktChildCollectionConfigBuilder&lt;TEntityType&gt;*

Adds a child collection to the current collection with the given names and description and default icons. A property accessor expression is required for both the entity ID field and FK (Foreign Key) field of the entity. See the [Child Collections API documentation](child-collections.md) for more info.

```csharp
// Example
collectionConfig.AddChildCollection<Child>(c => c.Id, c => c.ParentId, "Child", "Children", "A collection of children", childCollectionConfig => {
    ...
});
```

#### AddChildCollection&lt;TChildEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda childCollectionConfig = null) : *KonstruktChildCollectionConfigBuilder&lt;TEntityType&gt;*

Adds a child collection to the current collection with the given names, description and icons. A property accessor expression is required for both the entity ID field and FK (Foreign Key) field of the entity. See the [Child Collections API documentation](child-collections.md) for more info.

```csharp
// Example
collectionConfig.AddChildCollection<Child>(c => c.Id, c => c.ParentId, "Child", "Children", "A collection of children", "icon-umb-users", "icon-umb-users", childCollectionConfig => {
    ...
});
```