---
description: Configuring field renderers in Konstrukt, the back office UI builder for Umbraco.
---

# Field Renderers

Field Renderers allow you to customize the markup used by a field in a list view. Field Renderers are implemented as custom .NET Core View Components that are passed a single `KonstruktFieldRendererContext` argument with information about the entity / field being rendered. 

## Defining a field renderer

You can define a field renderer in one of two ways.

#### **1. A simple view file for the built in `KonstruktFieldRendererViewComponent` view component**

The simplest way to define a field renderer for non-complex renderers is to place a view file in the `/Views/Shared/Components/KonstruktFieldRenderer` folder with the following markup.

````csharp
@model Konstrukt.Web.Models.KonstruktFieldRendererContext
<!-- Insert your markup here -->
````

When registering a simple view file renderer you pass the name of the view file (excluding the `.cshtml` file extension) to the relevant API method.

#### **2. A completely custom view component**

To define a more complex field renderer you can create your own view component class (which can use dependency injection for any required dependencies) with the following signature

````csharp
// Example
public class MyComplexFieldRendererViewComponent : ViewComponent
{
    public async Task<IViewComponentResult> InvokeAsync(KonstruktFieldRendererContext context)
    {
        // Do your custom logic here

        return View("Default", model);
    }
}
````

For the view element of your component, based on the example above, you would place a file `Default.cshtml` into the  `/Views/Shared/Components/MyComplexFieldRenderer` folder with the following markup

````csharp
@model Namespace.Of.Model.Returned.By.Custom.ViewComponent
<!-- Insert your markup here -->
````

## KonstruktFieldRendererContext

Field renderer view components are passed a `KonstruktFieldRendererContext` context object with the following information.

````csharp
public class KonstruktFieldRendererContext
{
    public string FieldRenderer { get; set; }
    public object Entity { get; set; }
    public string PropName { get; set; }
    public object PropValue { get; set; }
}
````

## Setting the field renderer of a list view field

A field renderer is assigned to a list view field as part of the list view configuration. See [List View API Documentation](collection-list-views.md#setting-the-renderer-of-a-field) for more info.
