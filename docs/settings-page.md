# SettingsPage

The `SettingsPage` class contains locators and methods necessary to interact with the settings page.

## Members

### **Locators**

---

The locators used in the `SettingsPage` class aren't disclosed here, you can go through the `SettingsPage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`).

### **Methods**

---

There are a few methods in the `SettingsPage` class that are used to interact with the settings page. Some of the methods are private and some are public, italicized methods are private methods.

#### **CheckAliases**

---

The `CheckAliases` method is used to navigate to the company profile page, check for existing aliases, and add any new aliases that are not already present. This method ensures that all specified aliases are included in the company's profile. There are some methods which interact with the settings but are written in their corresponding `WebInteractions` class for modularity.

=== "Method Signature"

	```csharp
	public void CheckAliases(string aliases)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `aliases` | `string` | A comma-separated string containing the aliases to be checked and added to the company profile. |

=== "Functionality"

	1. **Navigate to Company Profile**: Go to the company profile URL.
	1. **Edit Company Profile**: Click the edit button to enable editing of the company profile.
	1. **Check and Add Aliases**: Split the input string into an array of aliases. For each alias:
		- Check if the alias is already present in the list of existing aliases.
		- If the alias is not present, add it to the list.
	1. **Save Changes**: Click the update button to save the changes to the company profile.
	1. **Confirm Update**: Confirm the update by clicking the proceed button and wait for the update to complete.

=== "Usage"

	This method is used in the `LCA Parsing` test script to ensure that all required aliases are present in the company profile.

	```csharp
	SettingsPage settingsPage = new SettingsPage();
	settingsPage.CheckAliases("Alias1, Alias2, Alias3");
	```

#### ***ValidateShowOrHideBtn***

---

The `ValidateShowOrHideBtn` method checks the functionality of "show" and "hide" password buttons in a web application. It validates that clicking these buttons correctly changes the password field's type attribute between "password" (hidden) and "text" (visible).


=== "Method Signature"

	```csharp
    private void ValidateShowOrHideBtn(string passwordBox, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `passwordBox` | `string` | The locator of the password input field. - "New Password" or "Confirm Password" |
	| `nodeName` | `string` | The name of the node to be shown on the Extent report. |

=== "Functionality"

	1. Locate Elements:
		- Define locators for the input field, show button, and hide button.
	1. Validate Initial State:
		- Wait for the password input field to be visible.
		- Retrieve and assert the initial type of the input field to be "password".
	1. Show Password:
		- Click the "show password" button.
		- Assert that the password input field type changes to "text".
	1. Hide Password:
		- Click the "hide password" button.
		- Assert that the password input field type changes back to "password".

=== "Usage"

	This method is used in the [`ChangePassword`](#changepassword) method to validate the functionality of the "show" and "hide" password buttons.

	=== "Example 1"
		```csharp
		SettingsPage settingsPage = new SettingsPage();
		settingsPage.ValidateShowOrHideBtn("New Password");
		```

	=== "Example 2"
		```csharp
		SettingsPage settingsPage = new SettingsPage();
		settingsPage.ValidateShowOrHideBtn("Confirm Password");
		```

#### **ChangePassword**

--- 

The ChangePassword method automates the process of changing a user's password. It includes steps for validating password guidelines, handling error messages, and ensuring that password requirements are met. This method uses the above [`ValidateShowOrHideBtn`](#validateshoworhidebtn)

=== "Method Signature"

	```csharp
	public void ChangePassword(string oldPassword, string newPassword, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `oldPassword` | `string` | The current password of the user. |
	| `newPassword` | `string` | The new password to be set for the user. |
	| `nodeName` | `string` | The name of the node to be shown on the Extent report. Default is `null` |

=== "Functionality"

	1. Navigate to Settings Page:
		- Navigate to the settings URL if the current URL does not match.
	1. Validate Password Guidelines:
		- Hover over the password guidelines button.
		- Ensure the tooltip contains specific text about password requirements and restrictions.
		- Assert that the tooltip text matches the expected guidelines.
	1. Attempt Save Without Data:
		- Click the "Save" button without entering any data.
		- Collect and assert error messages related to missing input.
	1. Test Error Messages for Incorrect Current Password:
		- Enter "test" into the current password field and verify the length requirement error.
		- Replace "test" with the actual old password and validate the password field.
	1. Validate Old and New Passwords:
		- Check error messages when old and new passwords are the same.
		- Enter and validate the new password in the new password field.
	1. Confirm New Password:
		- Check for error messages when new and confirm passwords do not match.
		- Enter and validate the new password in the confirm password field.
	1. Final Validation and Save:
		- Validate show/hide functionality for password fields.
		- Click the "Save" button and verify successful saving through a success message.