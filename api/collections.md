---
description: Configuring collections in Konstrukt, the back office UI builder for Umbraco.
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

## Defining filterable properties

Konstrukt will use filterable properties to dynamically build a filter dialog choosing an appropriate editor view for the property. Property of a number or date types will become range pickers, enums and properties with options defined will become select / checkbox lists and all other properties will become text input filters.

#### **AddFilterableProperty(Lambda filterablePropertyExpression, Lambda filterConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given property to the filterable properties collection.

````csharp
// Example
collectionConfig.AddFilterableProperty(p => p.FirstName, filterConfig => filterConfig 
    // ...
);
````

### Changing the label of a filterable property

#### **SetLabel(string label) : KonstruktFilterablePropertyConfigBuilder&lt;TEntityType, TValueType&gt;**

````csharp
// Example
filterConfig.SetLabel("First Name");
````

### Adding a description to a filterable property

#### **SetDescription(string description) : KonstruktFilterablePropertyConfigBuilder&lt;TEntityType, TValueType&gt;**

````csharp
// Example
filterConfig.SetDescription("The first name of the person");
````

### Defining basic options for a filterable property

#### **SetOptions(IDictionary&lt;TValueType, string&gt; options) : KonstruktFilterablePropertyConfigBuilder&lt;TEntityType, TValueType&gt;**

````csharp
// Example
filterConfig.SetOptions(new Dictionary<string, string> {
    { "Option1", "Option One" },
    { "Option2", "Option Two" }
});
````

### Defining options with custom compare clauses for a filterable property

#### **AddOption(object key, string label, Lambda compareExpresion) : KonstruktFilterablePropertyConfigBuilder&lt;TEntityType, TValueType&gt;**

````csharp
// Example
filterConfig.AddOption("Option1", "Option One", (val) => val != "Option Two");
````

### Configuring the mode of a filterable property

For filterable properties with options you can configure whether the options should be multiple or single choice.

#### **SetMode(KonstruktFilterMode mode) : KonstruktFilterablePropertyConfigBuilder&lt;TEntityType, TValueType&gt;**

````csharp
// Example
filterConfig.SetMode(KonstruktFilterMode.MultipleChoice);
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

## Defining data views

Data views allow you to define multiple, pre-filtered views of the same data source. This can be useful when entities exist in different states and you want a way to toggle between them.

#### **AddDataView(string name, Lambda whereClauseExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a data view with the given name and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.AddDataView("Active", p => p.IsActive);
````

#### **AddDataView(string group, string name, Lambda whereClauseExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a data view with the given group, name and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.AddDataView("Status", "Active", p => p.IsActive);
````

#### **SetDataViewsBuilder&lt;TDataViewsBuilder&gt;() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collections data views builder which allows you to define the data views dynamically at run time. See [Data Views Builders API documentation](data-views-builders.md) for more info.

````csharp
// Example
collectionConfig.SetDataViewsBuilder<PersonDataViewsBuilder>();
````

#### **SetDataViewsBuilder(Type dataViewsBuilderType) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collections data views builder which allows you to define the data views dynamically at run time. See [Data Views Builders API documentation](data-views-builders.md) for more info.

````csharp
// Example
collectionConfig.SetDataViewsBuilder(typeof(PersonDataViewsBuilder));
````

#### **SetDataViewsBuilder(KonstruktDataViewsBuilder&lt;TEntityType&gt; dataViewsBuilder) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collections data views builder which allows you to define the data views dynamically at run time. See [Data Views Builders API documentation](data-views-builders.md) for more info.

````csharp
// Example
collectionConfig.SetDataViewsBuilder(new PersonDataViewsBuilder());
````

## Adding an action

Actions allow you to perform custom tasks on one more entities in your collection. Actions can be accessed from a number of locations including the container / entity actions menu, the bulk actions bar and in indivdidual tables rows of a list view depending on the actions visibility.

#### **AddAction&lt;TMenuActionType&gt;() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds an action of the given type to the collection. See [Actions API documentation](actions.md) for more info.

````csharp
// Example
collectionConfig.AddAction<ExportMenuAction>();
````

#### **AddAction(Type actionType) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds an action of the given type to the collection. See [Actions API documentation](actions.md) for more info.

````csharp
// Example
collectionConfig.AddAction(actionType);
````

#### **AddAction(IKonstruktAction action) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given action to the collection. See [Actions API documentation](actions.md) for more info.

````csharp
// Example
collectionConfig.AddAction(action);
````

### Controlling an actions visibility

By default actions will be hidden unless they have a default visibility set on the action definition. You can also explicitly set an actions visibility as part of the `AddAction` API.

#### **AddAction&lt;TMenuActionType&gt;(Lambda actionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds an action of the given type to the collection with the given visibility. See [Actions API documentation](actions.md) for more info.

````csharp
// Example
collectionConfig.AddAction<ExportMenuAction>(actionConfig => actionConfig
    .SetVisibility(x => x.ActionType == KonstruktActionType.Bulk 
        || x.ActionType == KonstruktActionType.Row)
);
````

#### **AddAction(Type actionType, Lambda actionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds an action of the given type to the collection with the given visibility. See [Actions API documentation](actions.md) for more info.

````csharp
// Example
collectionConfig.AddAction(typeof(ExportMenuAction), actionConfig => actionConfig
    .SetVisibility(x => x.ActionType == KonstruktActionType.Bulk 
        || x.ActionType == KonstruktActionType.Row)
);
````

#### **AddAction(IKonstruktAction action, Lambda actionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given action to the collection with the given visibility. See [Actions API documentation](actions.md) for more info.

````csharp
// Example
collectionConfig.AddAction(action, actionConfig => actionConfig
    .SetVisibility(x => x.ActionType == KonstruktActionType.Bulk 
        || x.ActionType == KonstruktActionType.Row)
);
````

## Adding a card to a collection

Cards allow you to display simple summaries of key information that may be useful to the editor.

#### **AddCard(string name, Lambda whereClauseExpression, Lambda cardConfig = null) : KonstruktCardConfigBuilder**

Adds a card with the given name and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.AddCard("Older than 30", p => p.Age > 30, cardConfig => {
    ...
});
````

#### **AddCard(string name, string icon, Lambda whereClauseExpression, Lambda cardConfig = null) : KonstruktCardConfigBuilder**

Adds a card with the given name + icon and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.AddCard("Older than 30", "icon-umb-users", p => p.Age > 30, cardConfig => {
    ...
});
````

#### **AddCard<TCardType>() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a card of the given type to the collection. See [Card API documentation](cards.md) for more info.

````csharp
// Example
collectionConfig.AddCard<AvgPersonAgeCard>();
````

#### **AddCard(Type cardType) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds a card of the given type to the collection. See [Card API documentation](cards.md) for more info.

````csharp
// Example
collectionConfig.AddCard(typeof(AvgPersonAgeCard));
````

### Change the color of a card

#### **SetColor(string color) : KonstruktCardConfigBuilder**

Sets the color of the card.

````csharp
// Example
cardConfig.SetColor("blue");
````

### Add a suffix to a card value

#### **SetSuffix(string suffix) : KonstruktCardConfigBuilder**

Sets the suffix of the card value.

````csharp
// Example
cardConfig.SetSuffix("years");
````

### Formatting the value of a card

#### **SetFormat(Lambda formatExpression) : KonstruktCardConfigBuilder**

Sets the format expression for the card.

````csharp
// Example
cardConfig.SetFormat((v) => $"{v}%");
````

## Configuring the collection list view

#### **ListView(Lambda collectionConfig = null) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Accesses the list view config of the current collection. See [List View API documentation](collection-list-views.md) for more info.

````csharp
// Example
collectionConfig.ListView(collectionConfig => {
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