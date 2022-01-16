---
description: Differences between Konstrukt and UI-O-Matic, the back office UI builders for Umbraco.
---

# Konstrukt vs UI-O-Matic

For anyone familiar with Umbraco you may already know of the open source back office UI builder, UI-O-Matic and be wondering why you should choose Kostrukt instead. To help with that decision, we've put together the following feature matrix to compare some of their major differences.

## API

| | Konstrukt | UI-O-Matic|
| -- | -- | -- |
| Style | Fluent API | Attribute based API |
| Strongly Typed | Yes | No |
| Seperation of Concerns | Yes - Config is seperate to poco models | No - Config is combined with the poco models |
| Manage 3rd Party Models | Yes - As config is seperate to poco models, Konstrukt can manage any poco models | No - As config is attribute based, you need to have full control of poco models to add attributes to |
| Configuration Context | Config is always in the context of the poco model with Konstrukt atuomatically converting between properties and DB columns | Config switches between poco models properties and DB columns so can be confusing if you aren't aware of the context |
| Supports DI | Yes - Where types are passed to the API, the service provider is used to resolve those types allowing for dependency injection of depdendencies | No |


## Features

| | Konstrukt | UI-O-Matic |
| -- | -- | -- |
| Dashboards | Yes | No |
| Context Apps | Yes | Ish - There is an API to define context apps, but it's just a shortcut for Umbraco's context API, it doesn't support associating a collection with the context app |
| Sections | Yes | Yes - Requies custom tree controller |
| Section Dashboard | Yes | Yes |
| Cards | Yes | No |
| Data Views | Yes | Yes |
| Field Views | Format value only | Ability to format a value and provide a custom field view for custom vaue rendering |
| Field Editors | Konstrukt re-uses Umbraco property editors and so can use the full suite of core and community property editors | Limited to a set of UI-O-Matic provided editors |
| Editor Organisation Structure | Tabs + Fieldsets | Tabs |
| Menu Actions | Yes | Yes |
| Bulk Actions | Yes | No |
| Encrypted Properties | Yes | No |
| Value Mappers | Yes | No |
| Child Collections | Yes | Yes - Requires a convoluted config of hidden collections + list view properties on the parent poco model |
| Events | CRUD events | CRUD + Query events |
| Property Editors | Entity Picker | Dropdown + Multi Picker |

## License

| | Konstrukt | UI-O-Matic |
| -- | -- | -- |
| Open Source | No | Yes |
| Can be used on Umbraco Cloud | Yes | No |
| Fee | Free for one collection, then £450 exc VAT per install | Free unless you are and Umbraco Partner then you are required to negotiate a fee |

## Support

| | Konstrukt | UI-O-Matic |
| -- | -- | -- |
| Our Umbraco Forum | Yes | No |
| Email Support | Yes - Commercial | Yes - Personal |
| Issue Tracker | Yes | Yes |
