---
description: Configuring Konstrukt, the fluent administration panel builder for Umbraco.
---

# Configuration

Konstrukt can be configured in two ways, either directly via the `AddKonstrukt` extension method on `IUmbracoBuilder`, or via an `IKonstruktConfigurator` component registered with the DI container.

## AddKonstrukt

To configure Konstrukt via the `AddKonstrukt` extension method, you extend the `ConfigureServices` method found in the `Startup.cs` file of your web project. From within this method, between the call to `AddComposers()` and `Build()` we can add our `AddKonstrukt` configuration.

```csharp
public class Startup
{
    ...
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddUmbraco(_env, _config)
            .AddBackOffice()
            .AddWebsite()
            .AddComposers()
            .AddKonstrukt(cfg => {
                // Apply your configuration here
            })
            .Build();
    }
    ...
}

```

The `AddKonstrukt` extension method accepts a single parameter, a delegate function with a Konstrukt configuration builder on which you can call the relevant fluent API's to define your solution.

## IKonstruktConfigurator
