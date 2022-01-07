---
description: Configuring menu items in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Menu Items

Menu Items are a standard Umbraco concept and are used to configure items that appear in the list view / editor action menus.

## Defining a menu item

To define a menu item you create a class that inherits from the base class `KonstruktMenuItem` and configure it within the constructor like so.

````csharp
// Example
public class ExportMenuItem : KonstruktMenuItem
{
    public ExportMenuItem()
    {
        // Configure menu item
        Name = "Export";
        Alias = "export";
        Icon = "icon-download";

        // Set action behaviour
        Action = new KonstruktMenuItemRouteAction("/my/angular/route");
    }    
}
````

Available configuration options are:

* **Name:** The name of the menu item.
* **Alias:** A unique alias for the menu item.
* **Icon:** An icon to display next to the name in the menu.
* **SeperatorBefore:** Boolean flag to set whether to show a separator in the menu before this menu item.

In addition, menu items have an `Action` property of type `IKonstruktMenuItemAction` which can be one the following value types:

* **KonstruktMenuItemRouteAction(string route)** Navigates to the given route when clicked.
* **KonstruktMenuItemJavacriptAction(string jsAction)** Executes a javascript function when clicked.
* **KonstruktMenutItemDialogViewAction(string title, string view)** Opens an angular view in the left hand dialog modal, with the given title.
* **KonstruktMenutItemDialogUrlAction(string title, string url)** Opens a URL in an iframe in side the left hand dialog modal, with the given title.

As well as defining the menu item class, depending on the action type you configure, you will also need to implement the relevant angular view and controller. This is a little out of scope for the Konstrukt documentation, however in summary you will want to:

* Create a plugin folder in the root `App_Plugin` folder.
* Create a `package.manifest` file in your plugin folder.
* Create a html view to be loaded.
* Create an angular controller to control the view.
* Hook up the controller with the view using the `ng-controller` attribute.
* Add the controller js file path to the `package.manifest`.
* Build your custom logic.

## Adding a menu item to a collection

Menu items are added to a collection as part of the collections configuration. See [Collections API documentation](collections.md#defining-menu-items) for more info.