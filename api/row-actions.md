---
description: Configuring row actions in Konstrukt, the back office UI builder for Umbraco.
---

# Row Actions

Row actions provides an API to perform operations against individual items within a collections list view UI.

## Defining a row action

To define a row action you create a class that inherits from the base class `KonstruktRowAction<>` and configure it like so.

````csharp
// Example
public class MyRowAction : KonstruktRowAction<KonstruktActionResult>
{
    public override string Icon => "icon-settings";
    public override string Alias => "myaction";
    public override string Name => "My Action";
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

My default, actions will return a `KonstruktActionResult` but you can return other types of result by swapping the `KonstruktRowAction<>` generic argument.

* **`KonstruktActionResult`** - Standard result with a simple boolean `Success` value.
* **`KonstruktFileActionResult`** - Returns a file stream / bytes and triggers a download dialog.

## Configuraing action settings

Sometimes you may need to collect further user input before you can perform an action. To achieve this you can use the `KonstruktRowAction<>` base class that accepts an additional `TSetting` generic argument. 

````csharp
// Example
public class MyRowAction : KonstruktRowAction<MyRowActionSettings, KonstruktActionResult>
{
    public override string Icon => "icon-settings";
    public override string Alias => "myaction";
    public override string Name => "My Action";
    public override bool ConfirmAction => true;

    public override void Configure(KonstruktSettingsConfigBuilder<MyRowActionSettings> settingsConfig)
    {
        settingsConfig.AddFielset("General", fieldsetConfig => fieldsetConfig
            .AddField(s => s.RecipientName).SetLabel("Recipient Name")
            .AddField(s => s.ReceipientEmail).SetLabel("Recipient Email"))
    }

    public override KonstruktActionResult Execute(string collectionAlias, object entityId, MyRowActionSettings settings)
    {
        // Perform operation here...
    }
}

public class MyRowActionSettings
{
    public string ReceipientName { get; set; }
    public string ReceipientEmail { get; set; }
}
````

By implementing this base class you are required to implement an additional `Configure` method which accepts a `KonstruktSettingsConfigBuilder<>` parameter. You should use this parameter calling the builders fluent API to define the settings dialog UI and how it maps to the settings type. With the settings config builder you are able to create fieldsets and fields with the same fluent API as defined in the [editor section](collection-editors.md#adding-a-fieldset-to-a-tab).

In addition to this `Configure` method, your `Execute` method will also now accept an additional `settings` parameter of the settings type which will be pre-populated by Konstrukt with the value entered by the user allowing you to alter your actions behaviour accordingly.

## Adding a row action to a list view

Row actions are added to a list view as part of the list view configuration. See [List View API documentation](collection-list-views.md#adding-a-row-action) for more info.
