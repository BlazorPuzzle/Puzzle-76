# Puzzle #76 - Environments for Everyone!

Jeff and Carl want to know how to change up the environment configuration without swapping .json config files.

YouTube Video: https://youtu.be/

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
