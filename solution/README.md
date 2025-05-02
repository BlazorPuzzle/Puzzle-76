# Puzzle #76 - Environments for Everyone!

Jeff and Carl want to know how to change up the environment configuration without swapping .json config files.

YouTube Video: https://youtu.be/xxF8SkkTk1E

Blazor Puzzle Home Page: https://blazorpuzzle.com

## The Challenge

We received an email this week from a member of our Blazor community that's having some problems configuring a blazer application with different configuration settings that they they need to change between different environments.

```
My customer has two different environments (both in production AND development)
that require two sets of .json files for configuration.

Right now they are swapping file names in order to pick the environment. 

Is there an easier way?
```

We've mocked up a standard server-side-rendered Blazor application to explore this situation.  To demonstrate the scenario, we've added a configuration setting to **appsettings.json**:

```json
  "AllowWeather": false
```

There are checks for this configuration is **NavMenu.razor** and **Weather.razor** that will prevent the Weather navigation link from appearing as well as immediately redirect out of the Weather page if AllowWeather is set to false.

To complete a demo that emulates the scenario, we've added a file **Production.appsettings.json** using a similar naming as the customer that does enable the Weather pages.

How can the developers for this project work with these two configurations without having to play filename-rename-roulette?

## The Solution

ASP.NET Core has a rich configuration system that allows you to swap configurations based on the name of the environment.  By default, a machine with the .NET SDK installed and a **Properties/launchSettings.json** file has a directive to set the **ASPNETCORE_ENVIRONMENT** environment variable to **Development** when the application launches.

ASP.NET Core will optionally look for an appsettings.json file with the name **appsettings.{ENVIRONMENT}.json** and load those settings.  Rename the customer's production configuration file to **appsettings.Production.json**

On a production machine, this environment variable is not present and the default setting is **Production**.

To help with identifying these environments, we've added a helpful component called **EnvironmentRibbon** that will show the name of the environment in the top right corner of the page.  Try uncommenting this code in **MainLayout.razor**

```xml
@** Uncomment the below code **@
@* <EnvironmentRibbon /> *@

<div id="blazor-error-ui" data-nosnippet>
    An unhandled error has occurred.
    <a href="." class="reload">Reload</a>
    <span class="dismiss">🗙</span>
</div>
```

You can change the color of the ribbon by adding styles with a background color to the CSS classes with names like "corner-ribbon-production" or "corner-ribbon-development".  We added a green color for the development environment ribbon, and a default red color for the production environment.

More details about this feature can be found on learn at https://learn.microsoft.com/aspnet/core/fundamentals/configuration/?view=aspnetcore-9.0#appsettingsjson