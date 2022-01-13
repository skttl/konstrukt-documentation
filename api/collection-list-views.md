---
description: Configuring the list view of a collection in Konstrukt, the back office UI builder for Umbraco.
---

# List Views

A list view is a list based view of a collections entities providing such features as pagination for large collections, custom data views, searching and bulk actions.

## Configuring a list view

The list view configuration is a sub configuration of a [`Collection`](collections.md) config builder instance and is accessed via it's `ListView` method.

#### **ListView(Lambda listViewConfig = null) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Accesses the list view config of the given collection.

````csharp
// Example
collectionConfig.ListView(listViewConfig => {
    ...
});
````

## Changing the page size

#### **SetPageSize(int pageSize) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Sets the number of items to display per page for the given list view.

````csharp
// Example
listViewConfig.SetPageSize(20);
````

## Defining data views

Data views allow you to define multiple, pre-filtered views of the same data source which can be toggled between via the list view UI. This can be useful when entities exist in different states and you want a way to toggle between them.

#### **AddDataView(string name, Lambda whereClauseExpression) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Adds a data view with the given name and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
listViewConfig.AddDataView("Active", p => p.IsActive);
````

#### **AddDataView(string group, string name, Lambda whereClauseExpression) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Adds a data view with the given group, name and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
listViewConfig.AddDataView("Status", "Active", p => p.IsActive);
````

#### **SetDataViewsBuilder&lt;TDataViewsBuilder&gt;() : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Sets the list views data views builder which allows you to define the data views dynamically at run time. See [Data Views Builders API documentation](data-views-builders.md) for more info.

````csharp
// Example
listViewConfig.SetDataViewsBuilder<PersonDataViewsBuilder>();
````

#### **SetDataViewsBuilder(Type dataViewsBuilderType) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Sets the list views data views builder which allows you to define the data views dynamically at run time. See [Data Views Builders API documentation](data-views-builders.md) for more info.

````csharp
// Example
listViewConfig.SetDataViewsBuilder(typeof(PersonDataViewsBuilder));
````

#### **SetDataViewsBuilder(IKonstruktDataViewsBuilder dataViewsBuilder) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Sets the list views data views builder which allows you to define the data views dynamically at run time. See [Data Views Builders API documentation](data-views-builders.md) for more info.

````csharp
// Example
listViewConfig.SetDataViewsBuilder(new PersonDataViewsBuilder());
````

## Defining a bulk action

#### **AddBulkAction&lt;TBulkActionType&gt;() : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Adds a bulk action of the given type to the list view. See [Bulk Actions API documentation](bulk-actions/) for more info.

````csharp
// Example
listViewConfig.AddBulkAction<ExportBulkAction>();
````

#### **AddBulkAction(KonstruktBulkAction bulkAction) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Adds the provided bulk action to the list view. See [Bulk Actions API documentation](bulk-actions.md) for more info.

````csharp
// Example
listViewConfig.AddBulkAction(new ExportBulkAction());
````

## Changing the list view layout

By default the list view will use the built in Umbraco table and grid list view layouts however you can provide your own custom layouts. If you provide a layout, then it will replace the defaults, so if you still want the defaults as options, you'll need to add these again explicitly. To do this, you'll need to call `AddLayout<TListViewLayoutType>` for each one you want to add with a `TListViewLayoutType` parameter of `KonstruktTableListViewLayout` or `KonstruktGridListViewLayout`.

#### **AddLayout&lt;TListViewLayoutType&gt;() : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Adds a list view layout of the given type to the list view. See [List View Layouts API documentation](list-view-layouts.md) for more info.

````csharp
// Example
listViewConfig.AddLayout<MyCustomListViewLayout>();
````

#### **AddLayout(KonstruktListViewLayout listViewLayout) : KonstruktListViewConfigBuilder&lt;TEntityType&gt;**

Adds the provided list view layout to the list view. See [List View Layouts API documentation](list-view-layouts.md) for more info.

````csharp
// Example
listViewConfig.AddLayout(new MyCustomListViewLayout());
````

## Adding a field to the list view

#### **AddField(Lambda propertyExpression, Lambda propertyConfig = null) : KonstruktListViewFieldConfigBuilder&lt;TEntityType, TValueType&gt;**

Adds the given property to the list view.

````csharp
// Example
listViewConfig.AddField(p => p.FirstName, fieldConfig => {
    ...
});
````

## Changing the heading of a field

#### **SetHeading(string heading) : KonstruktListViewFieldConfigBuilder&lt;TEntityType, TValueType&gt;**

Sets the heading for the list view field.

````csharp
// Example
fieldConfig.SetHeading("First Name");
````

## Formatting the value of a field

#### **SetFormat(Lambda formatExpression) : KonstruktListViewFieldConfigBuilder&lt;TEntityType, TValueType&gt;**

Sets the format expression for the list view field.

````csharp
// Example
fieldConfig.SetFormat((v, p) => $"{v} years old");
````
