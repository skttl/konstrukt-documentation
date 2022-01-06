---
description: Configuring the editor of a collection in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Editor

An editor is the user interface used to edit an entity and is made up of tabs and property editors.

## Configuring an editor

The editor configuration is a sub configuration of a [`Collection`](collections.md) config builder instance and is accessing via it's `Editor` method.

#### Editor(Lambda editorConfig = null) : *KonstruktEditorConfig&lt;TEntityType&gt;*

Accesses the editor config of the given collection.

````csharp
// Example
collectionConfig.Editor(editorConfig => {
    ...
});
````

## Adding a tab to an editor

#### AddTab(string name, Lambda tabConfig = null) : *KonstruktTabConfigBuilder&lt;TEntityType&gt;*

Adds a tab to the editor.

````csharp
// Example
editorConfig.AddTab("General", tabConfig => {
    ...
});
````

## Adding a fieldset to a tab

#### AddFieldset(string name, Lambda fieldsetConfig = null) : *KonstruktEditorFieldTabConfigBuilder&lt;TEntityType, TValueType&gt;*

Adds the given fieldset to the tab.

````csharp
// Example
tabConfig.AddFieldset("Contact", fieldsetConfig => {
    ...
});
````

## Adding a field to a fieldset

#### AddField(Lambda propertyExpression, Lambda propertyConfig = null) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Adds the given property to the editor.

````csharp
// Example
fieldsetConfig.AddField(p => p.FirstName, fieldConfig => {
    ...
});
````

## Changing the label of a field

By default Konstrukt will build the label from the property name, including splitting camel case names into sentence case, however you can set an explicit label if you'd prefer.

#### SetLabel(string label) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Sets the label for the editor field.

````csharp
// Example
fieldConfig.SetLabel("First Name");
````

## Adding a description to a field

#### SetDescription(string description) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Sets the description for the editor field.

````csharp
// Example
fieldConfig.SetDescription("Enter your age in years");
````

## Setting the default value of a field

#### SetDefaultValue(TValueType defaultValue) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Sets the default value to a known constant.

````csharp
// Example
fieldConfig.SetDefaultValue(10);
````

#### SetDefaultValue(Func<TValueType> defaultValueFunc) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Sets the default value via a function that gets evaluated at time of entity creation.

````csharp
// Example
fieldConfig.SetDefaultValue(() => DateTime.Now);
````

## Making a field read only

#### MakeReadOnly() : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Makes the current field read only disabling editing in the UI. A ReadOnly property cannot have a custom DataType, ValueMapper or ValidationRegExp.

````csharp
// Example
fieldConfig.MakeReadOnly();
````

#### MakeReadOnly(Func&lt;TValueType, string&gt; format) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Makes the current field read only disabling editing in the UI. A ReadOnly property cannot have a custom DataType, ValueMapper or ValidationRegExp. Provides a custom formatting expression to use when rendering the value as a string.

````csharp
// Example
fieldConfig.MakeReadOnly(distanceProp => $"{distanceProp:## 'km'}");
````

## Making a field required

#### MakeRequired() : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Makes the given field required.

````csharp
// Example
fieldConfig.MakeRequired();
````

## Validating a field

#### SetValidationRegex(string regex) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Defines the regular expression to use when validating the field.

````csharp
// Example
fieldConfig.SetValidationRegex("[A-Z0-9._%+-]+@[A-Z0-9.-]+\\.[A-Z]{2,4}");
````

## Changing the data type of a field

By default Konstrukt will automatically choose a relevant data type for simple field types, however you can override this should you wish to use an alternative data type.

#### SetDataType(string dataTypeName) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Set the data type of the current field to the Umbraco data type with the given name.

````csharp
// Example
fieldConfig.SetDataType("Richtext Editor");
````

#### SetDataType(int dataTypeId) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Set the data type of the current field to the Umbraco data type with the given id.

````csharp
// Example
fieldConfig.SetDataType(-88);
````

## Setting a field value mapper

#### SetValueMapper&lt;TMapperType&gt;() : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Set the value mapper for the current field. See [Value Mapper API documentation](value-mappers.md) for more info.

````csharp
// Example
fieldConfig.SetValueMapper<MyValueMapper>();
````

#### SetValueMapper(KonstruktMapper mapper) : *KonstruktEditorFieldConfigBuilder&lt;TEntityType, TValueType&gt;*

Set the value mapper for the current field. See [Value Mapper API documentation](value-mappers.md) for more info.

````csharp
// Example
fieldConfig.SetValueMapper(new MyValueMapper());
````