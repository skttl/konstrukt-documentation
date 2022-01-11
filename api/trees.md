---
description: Configuring trees in Konstrukt, the back office UI builder for Umbraco.
---

# Trees

A tree is a hierarchical structure that helps organise a section into logical sub-sections and is accessed in the main side panel of the Umbraco interface. In Konstrukt, a section may only have a single tree definition, however you can use folder nodes to help organise the tree structure how you need it.

## Configuring a tree

The tree configuration is a sub configuration of a [`Section`](sections.md) config builder instance and is accessed via it's `Tree` method.

#### **Tree(Lambda treeConfig = null) : KonstruktTreeConfigBuilder**

Accesses the tree config of the given section.

````csharp
// Example
sectionConfig.Tree(treeConfig => {
    ...
});
````

## Adding a folder to a tree

#### **AddFolder(string name, Lambda folderConfig = null) : KonstruktFolderConfigBuilder**

Adds a folder to the current tree with the given name and a default folder icon. See the [Folders API documentation](folders.md) for more info.

```csharp
// Example
treeConfig.AddFolder("Settings", folderConfig => {
    ...
});
```

#### **AddFolder(string name, string icon, Lambda folderConfig = null) : KonstruktFolderConfigBuilder**

Adds a folder to the current tree with the given name + icon. See the [Folders API documentation](folders.md) for more info.

```csharp
// Example
treeConfig.AddFolder("Settings", "icon-settings", folderConfig => {
    ...
});
```

## Adding a collection to a tree

#### **AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, string nameSingular, string namePlural, string description, Lambda collectionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a collection to the current tree with the given names and description and default icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property. See the [Collections API documentation](collections.md) for more info.

```csharp
// Example
treeConfig.AddCollection<Person>(p => p.Id, "Person", "People", "A collection of people", collectionConfig => {
    ...
});
```

#### **AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda collectionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a collection to the current tree with the given names, description and icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property. See the [Collections API documentation](collections.md) for more info.

```csharp
// Example
treeConfig.AddCollection<Person>(p => p.Id, "Person", "People", "A collection of people", "icon-umb-users", "icon-umb-users", collectionConfig => {
    ...
});
```