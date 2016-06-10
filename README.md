# Testing .NET Core RC2 using NUnit 3

`dotnet-test-nunit` is the unit test runner for .NET Core for running
unit tests with NUnit 3.

## Usage

`dotnet-test-nunit` is still an alpha release, so you need to select `show prereleases` if you are using Visual Studio.

Your `project.json` in your test project should look like the following;

### project.json

```json
{
    "version": "1.0.0-*",

    "dependencies": {
        "NUnitWithDotNetCoreRC2": "1.0.0-*",
        "NETStandard.Library": "1.5.0-rc2-24027",
        "NUnit": "3.2.1",
        "dotnet-test-nunit": "3.4.0-alpha-1"
    },
    "testRunner": "nunit",

    "frameworks": {
        "netstandard1.5": {
            "imports": [
                "dnxcore50",
                "netcoreapp1.0",
                "portable-net45+win8"
            ]
        }
    },

    "runtimes": {
        "win10-x86": { },
        "win10-x64": { }
    }
}
```

The lines of interest here are the dependency on `dotnet-test-nunit`. Feel free to use the newest
version that is available. Note that the `NUnitWithDotNetCoreRC2` dependency is the project under test.

I have added `"testRunner": "nunit"` to specify NUnit 3 as the test adapter. I also had to add to the
imports for both the test adapter and NUnit to resolve. Lastly, I had to add the `runtimes`. If anyone can
explain why I need to do that, please let me know.

You can now run your tests using the Visual Studio Test Explorer, or by running `dotnet test` from the command
line.

```
# Restore the NuGet packages
dotnet restore

# Run the unit tests in the current directory
dotnet test

# Run the unit tests in a different directory
dotnet test .\test\NUnitWithDotNetCoreRC2.Test\
```

### Warning

Note that the `dotnet` command line swallows blank lines and does not work with color.
The NUnit test runner's output is in color, but you won't see it. These are known issues with
the `dotnet` CLI and not an NUnit bug.