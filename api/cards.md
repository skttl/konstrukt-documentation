---
description: Configuring cards in Konstrukt, the back office UI builder for Umbraco.
---

# Cards

Cards provide an API to display simple summary info on the list view UI. Simple cards can be defined inline as part of the [List View API](collection-list-views.md#adding-a-card-to-a-list-view) or can be defined using a `KonstruktCard` type to allow more control over the card value calculation.

When Konstrukt resolves a card it will attempt to do so from the global DI container which means you can inject amy dependencies that you require for your card to calculate it's value. If there is no such type defined in the DI container, Konstrukt will then fallback to maually instantiating a new instance of the card.

## Defining a card

To define a card you create a class that inherits from the base class `KonstruktCard` and configure it within the constructor like so.

````csharp
// Example
public class AvgPersonAgeCard : KonstruktCard
{
    public AvgPersonAgeCard()
    {
        Alias = "avgPersonAge";
        Name = "Average Age";
        Icon = "icon-calendar";
        Color = "green";
        Suffix = "yrs";
    }
        
    public override object GetValue(object parentId = null)
    {
        // Perform value calculation logic
    }
}
````

The required configuration options are:

* **Name:** The name of the card.
* **Alias:** A unique alias for the card.
* **GetValue(object parentId = null):** A method to get the cards value.

Additional optional configuration options are:

* **Icon:** An icon to display in the card.
* **Color:** The color of the card.
* **Suffix:** A suffix to display after the card value.

## Adding a card to a list view

A card is assigned to a list view as part of the list view configuration. See [List View API Documentation](collection-list-views.md#adding-a-card-to-a-list-view) for more info.