---
description: Configuring Sections in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Sections

A section is a distinct area of the Umbraco backoffice, such as content, media, etc, and is accessed via a link in the main menu at the top of the Umbraco interface. Konstrukt allows you to define multiple sections in order to organise the management of your models into logical sections.

## Defining a section

You define a section by calling one of the `AddSection` methods on the root level `KonstruktConfigBuilder` instance.

#### AddSection(string name, Lambda sectionConfig = null) : KonstruktSectionConfigBuilder

Adds a section to the Umbraco menu with the given name.

```csharp
// Example
config.AddSection("Database", sectionConfig => {
    ...
});
```

---

#### AddSectionBefore(string beforeAlias, string name, Lambda sectionConfig = null) : KonstruktSectionConfigBuilder

Adds a section to the Umbraco menu with the given name before the section with the given alias.

```csharp
// Example
config.AddSectionBefore("settings", "Database", sectionConfig => {
    ...
});
```

---

#### AddSectionAfter(string afterAlias, string name, Lambda sectionConfig = null) : KonstruktSectionConfigBuilder

Adds a section to the Umbraco menu with the given name after the section with the given alias.

```csharp
// Example
config.AddSectionAfter("media", "Database", sectionConfig => {
    ...
});
```