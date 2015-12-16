# nunit-specflow-plugin

SpecFlow plugin to inject custom properties into NUnit test cases.

## Installation

Reference SpecFlow plugin (*CTA.SpecFlowPlugin.dll*) in your configuration file (*app.config*):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <configSections>
    <section name="specFlow" type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler, TechTalk.SpecFlow" />
  </configSections>
  <specFlow>
    <unitTestProvider name="NUnit" />
    <plugins>
      <add name="Property" path="../packages/CTA.SpecFlowPlugin.1.0.0/lib" type="Generator" />
    </plugins>
  </specFlow>
</configuration>
```

## Usage

In a feature file (*.feature*) add property annotation using format `@PropertyName:PropertyValue`, see below:

```
@Capability:Chrome_Browser
Scenario: Google page is accessible
  Given I open Chrome
	When I navigate to menu 'http://google.com'
	Then Web page title should contains 'Google'
```

This will generate this NUnit code in *.feature.cs*:

```csharp
[NUnit.Framework.Property("Capability", "Chrome Browser")]
```

_Note_: No space around *:* and *_* in property value are replaced by spaces.
