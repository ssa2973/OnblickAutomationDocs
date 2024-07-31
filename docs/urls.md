# URLs

The `URLs` class is a singleton utility that constructs and provides access to various URLs used in the application under test. The URLs are derived from environment-specific configurations and endpoint definitions stored in JSON files. This class dynamically resolves base URLs based on the current environment and appends the appropriate endpoints.

## **Class Definition**

---

=== "URLs.cs"
```csharp
public class URLs
```

## **Properties**

---

=== "Instance"
	`Instance`: Provides access to the singleton instance of the URLs class.
	```csharp
	public static URLs Instance => _instance.Value;
	```
=== "GetUrl"
	`GetUrl(string domain, string endpointName)`: Constructs a complete URL by combining the specified domain with an endpoint from the configuration.
	```csharp

=== "Login_URL"
	`Login_URL`: URL for the login page.
	```csharp
	public string Login_URL => GetUrl(_mainDomain, nameof(Login_URL));
	```
	_Note: Other URL properties follow a similar pattern._


## **JSON Configuration**

---

The URLs are derived from two JSON files:
	- `endpoints-config.json`: Contains endpoint definitions for different environments.
	- `env-config.json`: Contains environment-specific configurations.

=== "Example `endpoints-config.json`"
	```json
	{
		"Timesheets_URL": "/app/employer-timesheets",
	    "Workforce_URL": "/app/workforce-new"
		// Additional endpoints as needed
	}
	```

=== "Example `env-config.json`"
	```json
	{
		"demo": {
			"main": <demo-base-url>,
			"hr": <hr-base-url>,
			"ess": <ess-base-url>
		},
		"prod": {
			"main": <prod-base-url>,
			//other similar properties as needed
		},
		"dev": {
			"main": <dev-base-url>,
			//other similar properties as needed
		}
		//other environments as needed
	}
	```


## **Usage**

---

To access URLs defined in the `URLs` class, use the singleton `Instance` to retrieve the desired URL property. The URL is constructed dynamically based on the current environment and the endpoint specified.

=== "Accessing Login URL"
	```csharp
	var loginUrl = URLs.Instance.Login_URL;
	```
=== "Accessing Workforce URL"
	```csharp
	var workforceUrl = URLs.Instance.Workforce_URL;
	```

## **Notes**

---

- The `env-config.json` file should define URLs for different environments such as `demo`, `prod`, etc.
- The `endpoints-config.json` file should include all necessary endpoint paths used throughout the application.