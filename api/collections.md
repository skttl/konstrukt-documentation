---
description: Configuring collections in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Collections

A collection is a container for a given data model and configures how the given model should display in a list view as well as how it should be edited.

## Defining a collection

You define a collection by calling one of the `AddCollection` methods on a given [`Tree`](trees.md) or parent [`Folder`](folders.md) config builder instance.

#### **AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, string nameSingular, string namePlural, string description, Lambda collectionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a collection to the given container with the given names and description and default icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property.

````csharp
// Example
folderConfig.AddCollection<Person>(p => p.Id, "Person", "People", "A collection of people", collectionConfig => {
    ...
});
````

#### **AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda collectionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a collection to the given container with the given names, description and icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property.

````csharp
// Example
folderConfig.AddCollection<Person>(p => p.Id, "Person", "People", "A collection of people", "icon-umb-users", "icon-umb-users", collectionConfig => {
    ...
});
````

## Changing a collection alias

#### **SetAlias(string alias) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the alias of the collection.  

**Optional:** When creating a new collection, an alias is automatically generated from the supplied name for you, however you can use the `SetAlias` method to override this should you need a specific alias.

````csharp
// Example
collectionConfig.SetAlias("person");
````

## Changing a collection icon color

#### **SetIconColor(string color) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collection icon color to the given color.  Possible options are `black`, `green`, `yellow`, `orange`, `blue` or `red`.

````csharp
// Example
collectionConfig.SetIconColor("blue");
````

## Changing a collection connection string

By default Konstrukt will use the Umbraco connection string for it's database connection however you can change this by calling the `SetConnectionString` method on a `Collection` config builder instance.

#### **SetConnectionString(string connectionStringName) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the connection string name for the given collection repository.

````csharp
// Example
collectionConfig.SetConnectionString("myConnectionStringName");
````

## Changing a collection repository implementation

By default Konstrukt will use a PetaPoco based repository for storing and fetching entities however you can implement your own repository should you need to store your entities via another strategy. To change the repository implementation used by a collection you can use the `SetRepositoryType` method. See [Repositories API documentation](repositories.md) for more info.

#### **SetRepositoryType&lt;TRepositoryType&gt;() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the repository type to the given type for the current collection.

````csharp
// Example
collectionConfig.SetRepositoryType<PersonRepositoryType>();
````

#### **SetRepositoryType(Type repositoryType) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the repository type to the given type for the current collection.

````csharp
// Example
collectionConfig.SetRepositoryType(typeof(PersonRepositoryType));
````

## Defining an entity name

Within Umbraco it is expected that an entity has a name property so we need to let Konstrukt know which property to use for the name or if our entity doesn't have a single name property, then how to construct a name from an entities other properties. We do this by using either the `SetNameProperty` or `SetNameFormat` methods on a `Collection` config builder instance.

#### **SetNameProperty(Lambda nameProperytyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets which property of your entity to use as the name property. Property must be of type `string`. By defining a property as the name property, it's value will be used as the label for the entity in things like trees and list views and will also be editable in the header region of the editor interface. The property will also automatically be added to the searchable properties collection and be used for the default sort property.

````csharp
// Example
collectionConfig.SetNameProperty(p => p.Name);
````

#### **SetNameFormat(Lambda nameFormatExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets a format expression to use to dynamically create a label for the entity in things like trees and list views. By providing a name format it is assumed there is no single name property available on the entity and as such none of the default behaviours descriped for the `SetNameProperty` method will apply.

````csharp
// Example
collectionConfig.SetNameFormat(p => $"{p.FirstName} {p.LastName}");
````

## Defining time stamp properties

#### **SetDateCreatedProperty(Lambda dateCreatedProperty) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets which property of our entity to use as the date created property. Property must be of type `DateTime`. When set and a new entity is saved via the Konstrukt repository, then the given field will be populated with the current date and time.

````csharp
// Example
collectionConfig.SetDateCreatedProperty(p => p.DateCreated);
````

#### **SetDateModifiedProperty(Lambda dateCreatedProperty) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets which property of our entity to use as the date modified property. Property must be of type `DateTime`. When set and an entity is saved via the Konstrukt repository, then the given field will be populated with the current date and time.

````csharp
// Example
collectionConfig.SetDateModifiedProperty(p => p.DateModified);
````

## Defining a deleted flag

By default in Konstrukt any entity that is deleted via the Konstrukt repository is completely removed from the system. In some occasions however you may wish to keep the records in the data repository but just mark them as deleted so that they don't appear in the UI. This is where the `SetDeletedProperty` method comes in handy.

#### **SetDeletedProperty(Lambda deletedPropertyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets which property of our entity to use as the deleted property flag. Property must be of type `boolean`. When a deleted property is set, any delete actions will set the deleted flag instead of actualy deleting the entity. In addition, any fetch actions will also pre-filter out any deleted entities.

````csharp
// Example
collectionConfig.SetDeletedProperty(p => p.Deleted);
````

## Defining a default sort order

#### **SetSortProperty(Lambda sortPropertyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets which property of our entity to sort against, defaulting to ascending sort direction.

````csharp
// Example
collectionConfig.SetSortProperty(p => p.FirstName);
````

#### **SetSortProperty(Lambda sortPropertyExpression, SortDirection sortDirection) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets which property of our entity to sort against in the provided sort direction.

````csharp
// Example
collectionConfig.SetSortProperty(p => p.FirstName, SortDirection.Descending);
````

## Defining searchable properties

#### **AddSearchableProperty(Lambda searchablePropertyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given property to the searchable properties collection. Property must be of type `String`. When set searches via the list view search and entity picker property editor search fields will search across the properties defined in this collection. If no properties are defined as searchable then these UI elements will be disabled.

````csharp
// Example
collectionConfig.AddSearchableProperty(p => p.FirstName);
````

## Defining encrypted properties

#### **AddEncryptedProperty(Lambda encryptedPropertyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given property to the encrypted properties collection. Property must be of type `String`. When set, the property will be encrypted/decrypted on write/read respectively.

````csharp
// Example
collectionConfig.AddEncryptedProperty(p => p.Email);
````

## Applying a global filter

Sometimes you may only want to work with a sub-set of data within a given table so this is where the `SetFilter` method comes in handy, allowing you to define a global filter to apply to all queries for the given collection.

#### **SetFilter(Lambda whereClauseExression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the filter where clause expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.SetFilter(p => p.Current);
````

## Defining menu items

#### **AddContainerMenuItem&lt;TMenuItemType&gt;() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a menu item of the given type to the collection tree node right click menu as well as the list view actions menu. See [Menu Items API documentation](menu-items.md) for more info.

````csharp
// Example
collectionConfig.AddContainerMenuItem<ExportMenuItem>();
````

#### **AddContainerMenuItem(MenuItem menuItem) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the provided menu item to the collection tree node right click menu as well as the list view actions menu. See [Menu Items API documentation](menu-items.md) for more info.

````csharp
// Example
collectionConfig.AddContainerMenuItem(new ExportMenuItem());
````

#### **AddEntityMenuItem&lt;TMenuItemType&gt;() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a menu item of the given type to the entity tree node right click menu as well as the entity editor actions menu. See [Menu Items API documentation](menu-items.md) for more info.

````csharp
// Example
collectionConfig.AddEntityMenuItem<ExportMenuItem>();
````

#### **AddEntityMenuItem(MenuItem menuItem) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the provided menu item to the entity tree node right click menu as well as the entity editor actions menu. See [Menu Items API documentation](menu-items.md) for more info.

````csharp
// Example
collectionConfig.AddEntityMenuItem(new ExportMenuItem());
````

## Showing a collection on the section dashboard

When navigating to a Konstrukt section you are automatically presented with a dashboard interface on which you can add your collections to. This dashboard gives a quick entry point to frequently used collections showing the number of items in the collection as well as links to it's list view as well as a quick create link (if the collection isn't read only).

{% hint style="info" %}
**NB:** Only section root level collections can be shown on the section dashboard.
{% endhint %}


#### **ShowOnDashboard() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collection to display on the section dashboard.

````csharp
// Example
collectionConfig.ShowOnDashboard();
````

## Making a collection read only

#### **MakeReadOnly() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collection as read only and disables any CRUD operations from being performed on the collection via the UI.

````csharp
// Example
collectionConfig.MakeReadOnly();
````

## Disable the option to create

#### **DisableCreate() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Disables the option to create entities on the current collection. An entity could be created via code-behind and then only editing is allowed in the UI for example.

````csharp
// Example
collectionConfig.DisableCreate();
````

## Disable the option to update

#### **DisableUpdate() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Disables the option to update entities on the current collection. An entity can be created, but further editing is not allowed. 

````csharp
// Example
collectionConfig.DisableUpdate();
````

## Disable the option to delete

#### **DisableDelete() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Disables the option to delete entities on the current collection. Useful if the data needs to be retained and visible. See also [defining a deleted flag](#defining-a-deleted-flag).

````csharp
// Example
collectionConfig.DisableDelete();
````

## Configuring the collection list view

#### **ListView(Lambda listViewConfig = null) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Accesses the list view config of the current collection. See [List View API documentation](collection-list-views.md) for more info.

````csharp
// Example
collectionConfig.ListView(listViewConfig => {
    ...
});
````

## Configuring the collection editor

#### **Editor(Lambda editorConfig = null) : KonstruktEditorConfigBuilder&lt;TEntityType&gt;**

Accesses the editor config of the current collection. See [Editor API documentation](collection-editors.md) for more info.

````csharp
// Example
collectionConfig.Editor(editorConfig => {
    ...
});
````

## Adding a child collection to a collection

#### **AddChildCollection&lt;TChildEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, Lambda childCollectionConfig = null) : KonstruktChildCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a child collection to the current collection with the given names and description and default icons. A property accessor expression is required for both the entity ID field and FK (Foreign Key) field of the entity. See the [Child Collections API documentation](child-collections.md) for more info.

```csharp
// Example
collectionConfig.AddChildCollection<Child>(c => c.Id, c => c.ParentId, "Child", "Children", "A collection of children", childCollectionConfig => {
    ...
});
```

#### **AddChildCollection&lt;TChildEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda childCollectionConfig = null) : KonstruktChildCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a child collection to the current collection with the given names, description and icons. A property accessor expression is required for both the entity ID field and FK (Foreign Key) field of the entity. See the [Child Collections API documentation](child-collections.md) for more info.

```csharp
// Example
collectionConfig.AddChildCollection<Child>(c => c.Id, c => c.ParentId, "Child", "Children", "A collection of children", "icon-umb-users", "icon-umb-users", childCollectionConfig => {
    ...
});
```

## Adding a child collection group to a collection

#### **AddChildCollectionGroup(string name, Lambda childCollectionGroupConfig = null) : KonstruktChildCollectionGroupConfigBuilder**

Adds a child collection group to the current collection with the given name and default icon. See the [Child Collections Group API documentation](child-collection-groups.md) for more info.

```csharp
// Example
collectionConfig.AddChildCollectionGroup("Family", childCollectionGroupConfig => {
    ...
});
```

#### **AddChildCollectionGroup(string name, string icon, Lambda childCollectionGroupConfig = null) : KonstruktChildCollectionGroupConfigBuilder**

Adds a child collection group to the current collection with the given name and icon. See the [Child Collections Group API documentation](child-collection-groups.md) for more info.

```csharp
// Example
collectionConfig.AddChildCollectionGroup("Family", "icon-users", childCollectionGroupConfig => {
    ...
});
```