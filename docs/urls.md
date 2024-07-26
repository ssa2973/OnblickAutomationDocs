# URLs

This class is used to store the URLs of the application under test. The URLs are stored as static endpoints in `endpoints-config.json` with a dynamic `baseurl` that depends on the `Environment` and can be accessed using the `Instance`.

=== "URLs.cs"
An overview of the `URLs` class is shown below:
```csharp 
public static URLs Instance => _instance.Value;
...
...
public string Login_URL => GetUrl(_mainDomain, nameof(Login_URL));
```

## Usage

To access any property in the `URLs` class, we first call the `URLs` class and then the `Environment`'s `Instance`. So it goes, `URLs.Instance.<Property-to-be-accessed>`

=== "Example 1"
	```csharp
	var loginUrl = URLs.Instance.Login_URL;
	```
=== "Example 2"
	```csharp
	var workforceUrl = URLs.Instance.Workforce_URL;
	```