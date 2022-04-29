---
description: Configuring a section dashboard in Konstrukt, the back office UI builder for Umbraco.
---

# Section Dashboards

A section dashboard is automatically displayed at the root of a Konstrukt defined section and it will display summaries of collections found within it that are told to display on the dashboard. It will also provide quick links to jump to that collections list view or to quickly add a new entry to that collection (if the collection isn't read only). 

![Section Dashboard](../images/section_dashboard.png)

## Showing a collection on a section dashboard

Showing a collection in the section dashboard is controlled via the collection configuration.

#### **ShowOnDashboard() : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Sets the collection to display on the section dashboard.

````csharp
// Example
collectionConfig.ShowOnDashboard();
````

{% hint style="info" %}
**NB:** Only section root level collections can be shown on the section dashboard.
{% endhint %}