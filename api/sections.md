---
description: Configuring Sections in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Sections

A section is a distinct area of the Umbraco backoffice, such as content, media, etc, and is accessed via a link in the main menu at the top of the Umbraco interface. Konstrukt allows you to define multiple sections in order to organise the management of your models into logical sections.

Each section defined via the Konstrukt API will also generate a tree in the UI under which your collections / folders will be added. All Konstrukt defined sections can only contain a single tree and so you can think of a Konstrukt section as being both a section and a tree configuration combined.

## Defining a section

You define a section by calling one of the `AddSection` methods on the root level `KonstruktConfigBuilder` instance.

#### AddSection(string name, Lambda sectionConfig = null) : *KonstruktSectionConfigBuilder*

Adds a section to the Umbraco menu with the given name.

```csharp
// Example
config.AddSection("Repositories", sectionConfig => {
    ...
});
```

#### AddSectionBefore(string beforeAlias, string name, Lambda sectionConfig = null) : *KonstruktSectionConfigBuilder*

Adds a section to the Umbraco menu with the given name before the section with the given alias.

```csharp
// Example
config.AddSectionBefore("settings", "Repositories", sectionConfig => {
    ...
});
```

#### AddSectionAfter(string afterAlias, string name, Lambda sectionConfig = null) : *KonstruktSectionConfigBuilder*

Adds a section to the Umbraco menu with the given name after the section with the given alias.

```csharp
// Example
config.AddSectionAfter("media", "Repositories", sectionConfig => {
    ...
});
```

## Changing a section alias

#### SetAlias(string alias) : *KonstruktSectionConfigBuilder*

Sets the alias of the section.

**Optional:** When adding a new section, an alias is automatically generated from the supplied name for you, however you can use the `SetAlias` method to override this should you need a specific alias.

```csharp
// Example
sectionConfig.SetAlias("repositories");
```

## Adding a folder to a section

#### AddFolder(string name, Lambda folderConfig = null) : *KonstruktFolderConfigBuilder*

Adds a folder to the current section with the given name and a default folder icon. See the [Folders API documentation](folders.md) for more info.

````csharp
// Example
sectionConfig.AddFolder("Settings", folderConfig => {
    ...
});
````

---

#### AddFolder(string name, string icon, Lambda folderConfig = null) : *KonstruktFolderConfigBuilder*

Adds a folder to the current section with the given name + icon. See the [Folders API documentation](folders.md) for more info.

````csharp
// Example
sectionConfig.AddFolder("Settings", "icon-settings", folderConfig => {
    ...
});