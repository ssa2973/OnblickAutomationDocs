# LoginCreds

The `LoginCreds` class is a singleton utility designed to manage and provide access to login credentials for HR Managers or Employers in various environments. The credentials are stored in a JSON file (`creds.json`) with environment-specific configurations and are accessed through the singleton Instance property.

## **Class Definition**

---

=== "LoginCreds.cs"
    ```csharp
    public class LoginCreds
    ```

## **Properties**

---

=== "Instance"

    - `Instance`: Provides access to the singleton instance of the LoginCreds class.
    
    ```csharp
    public static LoginCreds Instance => _instance.Value;
    ```

=== "HR_Email"

    - `HR_Email`: Retrieves the HR Manager's email address from the environment-specific JSON configuration.

    ```csharp
    public string HR_Email => _envConfig.GetProperty(nameof(HR_Email)).GetString();
    ```

=== "HR_Pwd"

    - `HR_Pwd`: Retrieves the HR Manager's password from the environment-specific JSON configuration.

    ```csharp
    public string HR_Pwd => _envConfig.GetProperty(nameof(HR_Pwd)).GetString();
	```

## **JSON Configuration**

---

The JSON configuration file contains login credentials for different environments. Here is a sample structure:

=== "creds.json"

    ```json
    {
      "demo": {
        "HR_Email": "<hr-email>",
        "HR_Pwd": "<hr-password>"
        // Additional credentials as needed for other organizations
      },
      "prod": {
        "HR_Email": "<hr-email>",
        "HR_Pwd": "<hr-password>"
        // Additional credentials as needed
      },
      "dev1": {
        // Environment-specific credentials
      },
      "dev2": {
        // Environment-specific credentials
      },
      "dev": {
        // Environment-specific credentials
      }
    }

    ```
    
## **Usage**

---

=== "Accessing Email"
	```csharp
	var hrEmail = LoginCreds.Instance.HR_Email;
	```
=== "Accessing Password"
	```csharp
	var hrPassword = LoginCreds.Instance.HR_Password;
	```

## **Notes**

---

   - The `creds.json` file contains 3 sets of credentials for different organizations in all environments.
   - There are multiple sets of credential details in `creds.json` to support different environments (e.g., `demo`, `prod`, `dev1`, `dev2`, `dev`).
   - Ensure that the correct environment is configured for the intended use case.
