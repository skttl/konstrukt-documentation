---
description: Controlling the visibility of actions in Konstrukt, the back office UI builder for Umbraco.
---

# Action Visibility

{% hint style="info" %}
**Work in Progress:** The documentation for this page is currently in progress.
{% endhint %}

## Controlling the default action visibility

Actions are not visible in the UI by default untill their visibility is configured. This can be done either at the action level, or at the registration level when adding the action to a collection. To define the default visbility of an action at the action level you can do this by overriding the `IsVisible` method of the `KonstruktAction<>` base class.

````csharp
// Example
public class MyAction : KonstruktAction<KonstruktActionResult>
{
    ...
    public override bool IsVisible(KonstruktActionVisibilityContext ctx)
    {
        return ctx.ActionType == KonstruktActionType.Bulk 
            || ctx.ActionType == KonstruktActionType.Row;
    }
    ...
}
````

The `IsVisible` method is passed a `KonstruktActionVisibilityContext` which contains an `ActionType` attribute defining the type of action that triggered this action handler to run as well as a `UserGroups` collection to allow you to manage visibility based on user permissions. You should use the information present in the `KonstruktActionVisibilityContext` object to decide whether the action should display, returning `true` if it should, or `false` if it should not. 


## Overriding an actions visibility

By default actions will be hidden unless they have a default visibility set on the action definition. You can also explicitly set an actions visibility as part of the `AddAction` API.

#### **AddAction&lt;TMenuActionType&gt;(Lambda actionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds an action of the given type to the collection with the given visibility.

````csharp
// Example
collectionConfig.AddAction<ExportMenuAction>(actionConfig => actionConfig
    .SetVisibility(x => x.ActionType == KonstruktActionType.Bulk 
        || x.ActionType == KonstruktActionType.Row)
);
````

#### **AddAction(Type actionType, Lambda actionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds an action of the given type to the collection with the given visibility.

````csharp
// Example
collectionConfig.AddAction(typeof(ExportMenuAction), actionConfig => actionConfig
    .SetVisibility(x => x.ActionType == KonstruktActionType.Bulk 
        || x.ActionType == KonstruktActionType.Row)
);
````

#### **AddAction(IKonstruktAction action, Lambda actionConfig = null) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given action to the collection with the given visibility.

````csharp
// Example
collectionConfig.AddAction(action, actionConfig => actionConfig
    .SetVisibility(x => x.ActionType == KonstruktActionType.Bulk 
        || x.ActionType == KonstruktActionType.Row)
);
````