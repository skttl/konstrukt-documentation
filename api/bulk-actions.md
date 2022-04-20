---
description: Configuring bulk actions in Konstrukt, the back office UI builder for Umbraco.
---

# Bulk Actions

Bulk actions provides an API to perform bulk operations from within a collections list view UI.

## Defining a bulk action

To define a bulk action you create a class that inherits from the base class `KonstruktBulkAction` and configure it like so.

````csharp
// Example
public class DeleteBulkAction : KonstruktBulkAction
{
    public override string Icon => "icon-trash";
    public override string Alias => "delete";
    public override string Name => "Delete";
    public override bool ConfirmAction => true;

    public override void Execute(string collectionAlias, object entityId)
    {
        // Perform operation here...
    }
}
````

The required configuration options are:

* **Name:** The name of the bulk action.
* **Alias:** A unique alias for the bulk action.
* **Icon:** An icon to display next to the name in the bulk action button.
* **Execute:** The method to run against a given entity.

Additional optional configuration options are:

* **ConfirmAction:** Set whether a confirm dialog should display before performing this action.

{% hint style="info" %}
You can use dependency injection to inject any services you require to perform your specific task. When injecting dependencies, it's always recomended that you inject `Lazy<YourService>` implementations of the required services to ensure they are only resolved when needed.
{% endhint %}

## Adding a bulk action to a list view

Bulk actions are added to a list view as part of the list view configuration. See [List View API documentation](collection-list-views.md#adding-a-bulk-action) for more info.
