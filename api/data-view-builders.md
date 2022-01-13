---
description: Configuring data view builders in Konstrukt, the back office UI builder for Umbraco.
---

# Data View Builders

Data views builders allow you to create a collection list views data views list dynamically at run time. By default Konstrukt will use the hard coded data views defined in your Konstrukt config, however if you need to build your data views list dynamically, then is is when you'd use a data views builder.

When Konstrukt resolves a data views builder it will attempt to do so from the global DI container which means you can inject amy dependencies that you require for your builder. If there is no such type defined in the DI container, Konstrukt will then fallback to maually instantiating a new instance of the data views builder.

## Defining a data views builder

To define a data views builder you create a class that inherits from the base class `KonstruktDataViewsBuilder<TEntityType>` and implements the abstract methods.

````csharp
// Example
public class PersonDataViewsBuilder : KonstruktDataViewsBuilder<Person>
{
    public override IEnumerable<KonstruktDataViewSummary> GetDataViews()
    {
        // Generate and return a list of data views
    }

    public override Expression<Func<Person, bool>> GetDataViewWhereClause(string dataViewAlias)
    {
        // Return a where clause expression for the supplied data view alias
    }
}
````

The required methods are:

* **GetDataViews:** Returns the list of data views to choose from.
* **GetDataViewWhereClause:** Returns the boolean where clause expression for the given data views alias.

## Setting the data views builder of a list view

A data views builder is assigned to a list view as part of the list view configuration. See [List View API Documentation](collection-list-views.md#defining-data-views) for more info.
