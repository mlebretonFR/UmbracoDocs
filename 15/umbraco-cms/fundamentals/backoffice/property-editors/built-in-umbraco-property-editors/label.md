# Label

`Schema Alias: Umbraco.Label`

`UI Alias: Umb.PropertyEditorUi.Label`

`Returns: String`

Label is a non-editable control and can only be used to display a pre-set value.

## Data Type Definition Example

![Label Data Type definition](images/Label-Setup.png)

### Value type

If you want to set a value other than a String, you can define the data using one of the other available Data Types. These include Decimal, Date/time, Time, Integer, and Big integer.

There is also a Value Type: Long string if you need to set a long string value for your Label.

## Content Example

![Label Content Example](../../../../../../10/umbraco-cms/fundamentals/backoffice/property-editors/built-in-property-editors/images/Label-Content-v8.png)

## MVC View Example

### Without Models Builder

```csharp
@{
    if (Model.HasValue("pageLabel")){
        <p>@(Model.Value("pageLabel"))</p>
    }
}
```

### With Models Builder

```csharp
@{
    if (!string.IsNullOrEmpty(Model.PageLabel))
    {
        <p>@Model.PageLabel</p>
    }
}
```

## Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the [Content Service](https://apidocs.umbraco.com/v15/csharp/api/Umbraco.Cms.Core.Services.ContentService.html).

{% hint style="info" %}
The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.
{% endhint %}

```csharp
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");
    
    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page
    
    // Set the value of the property with alias 'pageLabel'. 
    content.SetValue("pageLabel", "A pre-set string value");
    
    // Save the change
    ContentService.Save(content);
}
```

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

```csharp
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

```csharp
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'pageLabel'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MyLabel).Alias, "A pre-set string value");
}
```
