---
description: Configuring bulk actions in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Bulk Actions

Bulk actions provides an API to perform bulk operations from within a collections list view UI.

## Defining a bulk action

To define a bulk action you create a class that inherits from the base class `KonstruktBulkAction` and configure it within the constructor like so.

````csharp
// Example
public class DeleteBulkAction : KonstruktBulkAction
{
    public DeleteBulkAction()
    {
        // Configure bulk action
        Alias = "delete";
        Name = "Delete";
        Icon = "icon-trash";

        // Set the angular service to perform the bulk action
        AngularServiceName = "konstruktDeleteBulkActionService";
    }
}
````

The required configuration options are:

* **Name:** The name of the bulk action.
* **Alias:** A unique alias for the bulk action.
* **Icon:** An icon to display next to the name in the bulk action button.
* **AngularServiceName:** The name of the registered angular service to delegate the bulk action to.

## Defining a bulk action angular service

The actual logic for a bulk action needs to be encapsulated in an angular service with the following signature:

````javascript
(function () {

    'use strict';

    function KonstruktDeleteBulkAction(KonstruktResource) {

        return {
            
            performAction: function(collection, id) {
                return KonstruktResource.deleteEntity(collection, id);
            },

            getConfirmMessage: function (count) {
                return "Are you sure you want to delete " + count + " items?";
            },

            getProgressMessage: function(count, total) {
                return count + " of " + total + " items deleted";
            },

            getCompleteMessage: function(total) {
                return total + " items successfully deleted";
            }

        }

    }

    angular.module("umbraco.services").factory("konstruktDeleteBulkActionService", KonstruktDeleteBulkAction);

})();
````

The required service methods are:

* **performAction(section, collection, id)** Should perform the bulk action to the current item identified with the id parameter and return a promise.

The optional service methods are:

* **getConfirmMessage(count)** Should return a string to display as the confirmation message before the bulk action is performed. A generic default message will be used if no `getConfirmMessage` method is defined.
* **getProgressMessage(count, total)** Should return a string to display as the progress message whilst the bulk action is running. A generic default message will be used if no `getProgressMessage` method is defined.
* **getCompleteMessage(total)** Should return a string to display as the complete message once the bulk action has finished running. A generic default message will be used if no `getCompleteMessage` method is defined.

You'll need to ensure your angular service as well as any resources needed by your service are loaded before it can be used. This is a bit out of scope for the Konstrukt documentation, however in summary you will want to:

* Create a plugin folder in the root `App_Plugin` folder.
* Create a `package.manifest` file in your plugin folder.
* Add the service js file path to the `package.manifest`.

## Adding a bulk action to a list view

Bulk actions are added to a list view as part of the list view configuration. See [List View API documentation](collection-list-views.md#adding-a-bulk-action) for more info.
