# Setting Up the Environment

## Cloning the Repository
Clone the repository (if you have access to it) and navigate to the project's directory. You can clone it in two ways, one using the `git clone` command and the `Visual Studio` interface.

=== "Using Visual Studio"
	1. Open Visual Studio.
	2. Click on `Clone a repository`.
	3. Enter the repository URL `https://onblickrigaps.visualstudio.com/Automation/_git/Selenium2.0`.
	4. Click on `Clone`.

=== "Using Terminal"
	```bash
	git clone https://onblickrigaps.visualstudio.com/Automation/_git/Selenium2.0
	```

After you finish cloning, the setup should be complete.

## Changing the environment tests are running on

In `Environment.cs` you can change the environment the tests are running on. The default environment is `demo`.

=== "Environment.cs"
	```csharp
	public static string Name => System.Environment.GetEnvironmentVariable("ENVIRONMENT") ?? "demo";
	```

=== "Allowed values for Environment variable"

	Allowed values for `ENVIRONMENT` or `Environment.Name` are `demo`, `dev`, `prod`, `dev1`, `dev2`.

### Setting the Environment variable

_This `ENVIRONMENT` variable is also used in the pipeline to control which environment the tests are being executed on._

![Environment Variable](./assets/images/env.png)
