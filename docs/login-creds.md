# LoginCreds

This class is used to store the login credentials of the `HR Manager` or `Employer` under test. The credentials are stored as static variables in `creds.json` with a dynamic environment-based assignment and can be accessed using the `Instance`.

=== "LoginCreds.cs"

```csharp 
public static LoginCreds Instance => _instance.Value;
...
...
public string HR_Email => _envConfig.GetProperty(nameof(HR_Email)).GetString();
```

## Usage

=== "Email"
	```csharp
	var hrEmail = LoginCreds.Instance.HR_Email;
	```
=== "Password"
	```csharp
	var hrPassword = LoginCreds.Instance.HR_Password;
	```

_Note: There are three separate sets of credential details in creds.json, each arranged for different organizations._
