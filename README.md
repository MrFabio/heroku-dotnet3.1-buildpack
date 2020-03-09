# .NET Core 3.1+ Buildpack
This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpack) for building [.NET Core](https://www.microsoft.com/net/core) apps using [`.csproj` files](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/project-json).

**Please note:** 
This buildpack is an experimental project and is not officially supported.


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*based on [.NET Core 2.0+ Buildpack](https://github.com/MrFabio/heroku-dotnet2.0-buildpack-vs2017)*

**Versions**

	Node.js      - 12.16.1 LTS
	.Net SDK     - 3.1.102 LTS
	.Net Runtime - 3.1.2
	
## Usage with HerokuCLI [(link)](https://devcenter.heroku.com/articles/heroku-cli)

Example usage (create a new application on heroku):

    $ heroku create --buildpack https://github.com/MrFabio/heroku-dotnet2.0-buildpack-vs2017.git
    $ git push heroku master

**How to bring back your application to [Heroku-18](https://devcenter.heroku.com/articles/heroku-18-stack) (with Heroku CLI):**

    $ heroku stack:set Heroku-18 [--remote xxx]

The buildpack will detect your app as .NET Core if it has `.csproj`. 

If the source code you want to build contains multiple `.csproj` files, 
it will compile the `.csproj` that has the same name of your solution file `.sln`.

## Buildpack will publish your project as "Release" Build

    dotnet publish ${PROJECT_FILE} --output ${BUILD_DIR} --runtime ubuntu.14.04-x64 --configuration Release

## NuGet - If additional Package Sources needed

When `dotnet restore` is called for restore NuGet packages, `NuGet.Config` placed in root directory will be used. 
You can specify additional `<packageSources>` like in the following example.

Example `NuGet.Config`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="NuGet" value="https://api.nuget.org/v3/index.json" />
	<add key="xxx" value="https://xxx/index.json" />
    <add key="yyy" value="https://yyy/index.json" />
  </packageSources>
</configuration>
```
