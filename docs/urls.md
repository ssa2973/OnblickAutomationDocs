# URLs

This class is used to store the URLs of the application under test. The URLs are stored as static endpoints in `endpoints-config.json` with a dynamic baseurl that depends on the Environment and can be accessed using the `Instance`.

=== "URLs.cs"
```csharp 
public static URLs Instance => _instance.Value;
...
...
public string Login_URL => GetUrl(_mainDomain, nameof(Login_URL));
```

## Usage

=== "Example 1"
	```csharp
	var loginUrl = URLs.Instance.Login_URL;
	```
=== "Example 2"
	```csharp
	var workforceUrl = URLs.Instance.Workforce_URL;
	```