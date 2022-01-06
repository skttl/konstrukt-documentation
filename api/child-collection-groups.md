---
description: Configuring child collection groups in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Child Collection Groups

A child collection group is a container for other child collections. It's purpose is mainly to provide a logical grouping of multiple child collections to help with organisation and an improved user experience.

## Defining a child collection group

You define a child collection group by calling one of the `AddChildCollectionGroup` methods on a given [`Collection`](collections.md) config builder instance.

#### AddChildCollectionGroup(string name, Lambda childCollectionGroupConfig = null) : *KonstruktChildCollectionGroupConfigBuilder*

Adds a child collection group to the current collection with the given name and default icon.

```csharp
// Example
collectionConfig.AddChildCollectionGroup("Family", childCollectionGroupConfig => {
    ...
});
```

#### AddChildCollectionGroup(string name, string icon, Lambda childCollectionGroupConfig = null) : *KonstruktChildCollectionGroupConfigBuilder*

Adds a child collection group to the current collection with the given name and icon.

```csharp
// Example
collectionConfig.AddChildCollectionGroup("Family", "icon-users", childCollectionGroupConfig => {
    ...
});
```

## Adding a child collection to a child collection group

#### AddChildCollection&lt;TChildEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, Lambda childCollectionConfig = null) : *KonstruktChildCollectionConfigBuilder&lt;TEntityType&gt;*

Adds a child collection to the current collection with the given names and description and default icons. A property accessor expression is required for both the entity ID field and FK (Foreign Key) field of the entity. See the [Child Collections API documentation](child-collections.md) for more info.

```csharp
// Example
childCollectionGroupConfig.AddChildCollection<Child>(c => c.Id, c => c.ParentId, "Child", "Children", "A collection of children", childCollectionConfig => {
    ...
});
```

#### AddChildCollection&lt;TChildEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda childCollectionConfig = null) : *KonstruktChildCollectionConfigBuilder&lt;TEntityType&gt;*

Adds a child collection to the current collection with the given names, description and icons. A property accessor expression is required for both the entity ID field and FK (Foreign Key) field of the entity. See the [Child Collections API documentation](child-collections.md) for more info.

```csharp
// Example
childCollectionGroupConfig.AddChildCollection<Child>(c => c.Id, c => c.ParentId, "Child", "Children", "A collection of children", "icon-umb-users", "icon-umb-users", childCollectionConfig => {
    ...
});
```