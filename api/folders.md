---
description: Configuring folders to organise sections in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Folders

A folder appears in a section tree and is used to help organise the tree structure by grouping things together. Folders can be added to a section or any other folder and can contain either other (sub)folders or [collections](collections.md).

## Defining a folder

You define a folder by calling one of the `AddFolder` methods on a given [`Section`](sections.md) or parent `Folder` builder instance.

#### AddFolder(string name, Lambda folderConfig = null) : *KonstruktFolderConfigBuilder*

Adds a folder to the current tree with the given name and a default folder icon.

````csharp
// Example
treeConfig.AddFolder("Settings", folderConfig => {
    ...
});
````

#### AddFolder(string name, string icon, Lambda folderConfig = null) : *KonstruktFolderConfigBuilder*

Adds a folder to the current tree with the given name + icon.

````csharp
// Example
treeConfig.AddFolder("Settings", "icon-settings", folderConfig => {
    ...
});
````

## Changing a folder alias

#### SetAlias(string alias) : *KonstruktFolderConfigBuilder*

Sets the alias of the folder.  

**Optional:** When creating a new folder, an alias is automatically generated from the supplied name for you, however you can use the `SetAlias` method to override this should you need a specific alias.

````csharp
// Example
folderConfig.SetAlias("settings");
````

## Changing a folder icon color

#### SetIconColor(string color) : *KonstruktFolderConfigBuilder*

Sets the folder icon color to the given color.  Possible options are `black`, `green`, `yellow`, `orange`, `blue` or `red`.

````csharp
// Example
folderConfig.SetIconColor("blue");
````

## Adding a sub folder to a folder

#### AddFolder(string name, Lambda folderConfig = null) : *KonstruktFolderConfigBuilder*

Adds a sub folder to the current folder with the given name and a default folder icon.

````csharp
// Example
folderConfig.AddFolder("Categories", subFolderConfig => {
    ...
});
````

#### AddFolder(string name, string icon, Lambda folderConfig = null) : *KonstruktFolderConfigBuilder*

Adds a sub folder to the current folder with the given name + icon.

````csharp
// Example
folderConfig.AddFolder("Categories", "icon-tags", subFolderConfig => {
    ...
});
````

## Adding a collection to a folder

#### AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, string nameSingular, string namePlural, string description, Lambda collectionConfig = null) : *KonstruktCollectionConfigBuilder&lt;TEntityType&gt;*

Adds a collection to the current folder with the given names and description and default icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property. See the [Collections API documentation]({{ site.baseurl }}/api/collections/) for more info.

````csharp
// Example
folderConfig.AddCollection<Person>(p => p.Id, "Person", "People", "A collection of people", collectionConfig => {
    ...
});
````

#### AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda collectionConfig = null) : *KonstruktCollectionConfigBuilder&lt;TEntityType&gt;*

Adds a collection to the current folder with the given names, description and icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property. See the [Collections API documentation]({{ site.baseurl }}/api/collections/) for more info.

````csharp
// Example
folderConfig.AddCollection<Person>(p => p.Id, "Person", "People", "A collection of people", "icon-umb-users", "icon-umb-users", collectionConfig => {
    ...
});
````
