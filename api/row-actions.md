---
description: Configuring row actions in Konstrukt, the back office UI builder for Umbraco.
---

# Row Actions

Row actions provides an API to perform operations against individual items within a collections list view UI.

## Defining a row action

To define a row action you create a class that inherits from the base class `KonstruktRowAction<>` and configure it like so.

````csharp
// Example
public class DeleteRowAction : KonstruktRowAction<KonstruktActionResult>
{
    public override string Icon => "icon-trash";
    public override string Alias => "delete";
    public override string Name => "Delete";
    public override bool ConfirmAction => true;

    public override KonstruktActionResult Execute(string collectionAlias, object entityId)
    {
        // Perform operation here...
    }
}
````

The required configuration options are:

* **Name:** The name of the row action.
* **Alias:** A unique alias for the row action.
* **Icon:** An icon to display next to the name in the row action button.
* **Execute:** The method to run against a given entity.

Additional optional configuration options are:

* **ConfirmAction:** Set whether a confirm dialog should display before performing this action.

The generic argument is a return type for the action. See [Controlling the action result](#controlling-the-action-result) below.

{% hint style="info" %}
You can use dependency injection to inject any services you require to perform your specific task. When injecting dependencies, it's always recomended that you inject `Lazy<YourService>` implementations of the required services to ensure they are only resolved when needed.
{% endhint %}

## Controlling the action result

My default, actions will return a basic `KonstruktActionResult` which has a simple boolean `Success` property, but you can return other types depending on the behaviour your require.

* **`KonstruktFileActionResult`** - Returns a file stream / bytes and triggers a download dialog.

## Adding a row action to a list view

Row actions are added to a list view as part of the list view configuration. See [List View API documentation](collection-list-views.md#adding-a-row-action) for more info.
