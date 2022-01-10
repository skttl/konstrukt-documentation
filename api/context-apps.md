---
description: Configuring context apps in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Context Apps

Context Apps in Konstrukt are analogous with Content Apps in Umbraco and they allow you provide contextual apps that appear in the editor of other contextApps of the Umbraco CMS. From a Konstrukt perspective, defining context apps allows you to expose collections as content app where a collection has a relation to the content in question. An example could be something like blog post comments which are linked to individual blog posts. By exposing these as a content app allows them to be managed in context next to the blog post they are linked to.

## Defining a context app

You define a context app by calling one of the `AddContextApp` methods on the root level `KonstruktConfigBuilder` instance.

#### **AddContextApp(string name, Lambda contextAppConfig = null) : KonstruktContextAppConfigBuilder**

Adds a contextApp with the given name and default icon.

```csharp
// Example
config.AddContextApp("Comments", contextAppConfig => {
    ...
});

#### **AddContextApp(string name, string icon, Lambda contextAppConfig = null) : KonstruktContextAppConfigBuilder**

Adds a contextApp to the Umbraco menu with the given name and icon.

```csharp
// Example
config.AddContextApp("Comments", "icon-chat", contextAppConfig => {
    ...
});

## Changing a context app alias

#### **SetAlias(string alias) : KonstruktContextAppConfigBuilder**

Sets the alias of the contextApp.

**Optional:** When adding a new context app, an alias is automatically generated from the supplied name for you, however you can use the `SetAlias` method to override this should you need a specific alias.

```csharp
// Example
contextAppConfig.SetAlias("comments");
```

## Changing a context app icon color

#### **SetIconColor(string color) : KonstruktContextAppConfigBuilder**

Sets the context app icon color to the given color.  Possible options are `black`, `green`, `yellow`, `orange`, `blue` or `red`.

````csharp
// Example
contextAppConfig.SetIconColor("blue");
````

## Changing the position of a context app

Changing the position of a context app in the UI is done by modiying it's weight. Default content apps `Content` and `Info` have the weights `-100` and `100` respectively.

#### **SetWeight(int weight) : KonstruktContextAppConfigBuilder**

Sets the context app weight to the given value. 

````csharp
// Example
contextAppConfig.SetWeight(10);
````

## Changing when a context app should display

Changing when a context app is displayed is controlled by a delegate method which is passed a `KonstruktContextAppVisibilityContext` instance which contains a `Source` property which holds a reference to the source object that content app is being displayed on (ie, an `IContent` instance) and a `UserGroups` collection of the current logged in users user groups. You can use an value from those to return a boolean result which sets whether to display the context app or not.

#### **SetVisibility(Func&lt;KonstruktContextAppVisibilityContext, bool&gt; visibilityExpression) : KonstruktContextAppConfigBuilder**

Sets the context app visibility delegate. 

````csharp
// Example
contextAppConfig.SetVisibility(appCtx => appCtx.Source is IContent content && content.ContentType.Alias == "blogPost");
````

# Adding a collection to a context app

Context apps can consist of one or more collections. If a context app contains multiple collections, the collection list views will be displayed in tabs within the context app.

#### **AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, Lambda collectionConfig = null) : KonstruktContextAppConfigBuilder**

Adds a collection to the current tree with the given names and description and default icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property. A foreign key property accessor is also required so that Konstrukt knows which property holds the Umbraco nodes UDI value. See the [Collections API documentation](collections.md) for more info.

```csharp
// Example
contextAppConfig.AddCollection<Comment>(p => p.Id, p=> "Comment", "Comments", "A collection of comments", collectionConfig => {
    ...
});
```

#### **AddCollection&lt;TEntityType&gt;(Lambda idFieldExpression, Lambda fkFieldExpression, string nameSingular, string namePlural, string description, string iconSingular, string iconPlural, Lambda collectionConfig = null) : KonstruktContextAppConfigBuilder**

Adds a collection to the current tree with the given names, description and icons. An ID property accessor expression is required so that Konstrukt knows which property is the ID property. A foreign key property accessor is also required so that Konstrukt knows which property holds the Umbraco nodes UDI value. See the [Collections API documentation](collections.md) for more info.

```csharp
// Example
contextAppConfig.AddCollection<Comment>(p => p.Id, "Comment", "People", "A collection of comments", "icon-chat", "icon-chat", collectionConfig => {
    ...
});
```