---
description: Configuring Konstrukt, the fluent back office UI builder for Umbraco.
---

# Configuration

Konstrukt can be configured in two ways, either directly via the `AddKonstrukt` extension method on `IUmbracoBuilder`, or via an `IKonstruktConfigurator` component registered with the DI container.

## AddKonstrukt

To configure Konstrukt via the `AddKonstrukt` extension method, you extend the `ConfigureServices` method found in the `Startup.cs` file in the root of your web project. From within this method, between the call to `AddComposers()` and `Build()` we can add our `AddKonstrukt` configuration.

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

The `AddKonstrukt` extension method accepts a single parameter, a delegate function with a Konstrukt configuration builder argument on which you can call the relevant fluent API's to define your solution.

See the [API section](../api/conventions.md) for information on the various configuration methods available on the config builder.

## IKonstruktConfigurator

To configure Konstrukt vis a `IKonstruktConfigurator` you can create a class anywhere in your project that inherits from the `IKonstruktConfigurator` interface and Konstrukt will automatically find them and register their configurations with the DI container.

```csharp
public class MyKonstruktConfigurator : IKonstruktConfigurator
{
    public void Configure(KonstruktConfigBuilder builder)
    {
        // Apply your configuration here
    }
}
```

The `IKonstruktConfigurator` has a single `Configure` method with a single Konstrukt configuration builder argument on which you can call the relevant fluent API's to define your solution.

See the [API section](../api/conventions.md) for information on the various configuration methods available on the config builder.
