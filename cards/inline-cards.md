---
description: Configuring inline cards in Konstrukt, the back office UI builder for Umbraco.
---

# Inline Cards

{% hint style="info" %}
**Work in Progress:** The documentation for this page is currently in progress.
{% endhint %}

## Adding an inline card to a collection

Cards allow you to display simple summaries of key information that may be useful to the editor.

#### **AddCard(string name, Lambda whereClauseExpression, Lambda cardConfig = null) : KonstruktCardConfigBuilder**

Adds a card with the given name and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.AddCard("Older than 30", p => p.Age > 30, cardConfig => {
    ...
});
````

#### **AddCard(string name, string icon, Lambda whereClauseExpression, Lambda cardConfig = null) : KonstruktCardConfigBuilder**

Adds a card with the given name + icon and where clause filter expression. Expression must be a `boolean` expression.

````csharp
// Example
collectionConfig.AddCard("Older than 30", "icon-umb-users", p => p.Age > 30, cardConfig => {
    ...
});
````

### Change the color of a card

#### **SetColor(string color) : KonstruktCardConfigBuilder**

Sets the color of the card.

````csharp
// Example
cardConfig.SetColor("blue");
````

### Add a suffix to a card value

#### **SetSuffix(string suffix) : KonstruktCardConfigBuilder**

Sets the suffix of the card value.

````csharp
// Example
cardConfig.SetSuffix("years");
````

### Formatting the value of a card

#### **SetFormat(Lambda formatExpression) : KonstruktCardConfigBuilder**

Sets the format expression for the card.

````csharp
// Example
cardConfig.SetFormat((v) => $"{v}%");
````