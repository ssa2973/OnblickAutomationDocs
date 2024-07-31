# LoginPage

The `LoginPage` class contains all the locators and methods necessary to interact with the login page.

## Members

### **Locators**


---

The locators used in the `LoginPage` class aren't disclosed here, you can go through the `LoginPage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`). 

### **Methods**

---

There are several methods in the `LoginPage` class that are used to interact with the login page. Some of the methods are private and some are public, italicized methods are private methods.

#### **ValidLogin**

---

This method is used to login to the application with valid credentials (HR or ESS).

=== "Method Signature"

	```csharp
	public void ValidLogin(string user, string pass, string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `user` | `string` | The username to be entered in the `username` field. |
	| `pass` | `string` | The password to be entered in the `password` field. |
	| `nodeName` | `string` | The name of the node to be shown on the Extent report. |

=== "Functionality"

	1. Navigate to the login page.
	1. Hover and click on the `HR Immigration` or `ESS` button.
	1. Enter the username and password.
	1. Click the login button.
	1. Wait until the url contains `dashboard`.

#### **InvalidLogin**

---

This method is used to check login to the application with invalid credentials.

=== "Method Signature"

	```csharp
	public void InvalidLogin(string user, string pass, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `user` | `string` | The username to be entered in the `username` field. |
	| `pass` | `string` | The password to be entered in the `password` field. |
	| `nodeName` | `string` | The name of the node to be shown on the Extent report. |

=== "Functionality"

	1. Navigate to the login page.
	1. Hover and click on the `HR Immigration` or `ESS` button.
	1. Enter the username and password.
	1. Click the login button.
	1. Wait until the error message is displayed.

#### **LogOut**

---

This method is used to logout from the application.

=== "Method Signature"

	```csharp
	public void LogOut(string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the node to be shown on the Extent report. |

=== "Functionality"

	1. Click on the user icon.
	1. Click on the logout button.
	1. Wait until the url is `Login__URl`.

#### ***ResetPassword***

---

This private method is used in [ResetPasswordESS](#resetpasswordess) method which takes in some functions as parameter and can be used access the reset password page from mail in any of the mail pages (`MailhogPage` or `MailinatorPage`).

=== "Method Signature"

	```csharp
    private void ResetPassword(IWebDriver driver, string url, Func<By> resetIdFunc, Func<By> resetBtnIdFunc, Action getIFrameFunc, Action<string> searchBarFunc, string email)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | `IWebDriver` | The driver instance. |
	| `url` | `string` | The url of the mail page. |
	| `resetIdFunc` | `Func<By>` | The function to get the reset password link locator. |
	| `resetBtnIdFunc` | `Func<By>` | The function to get the reset password button locator. |
	| `getIFrameFunc` | `Action` | The function to switch to the iframe. |
	| `searchBarFunc` | `Action<string>` | The function to search for the email. |
	| `email` | `string` | The email to be searched. |

=== "Functionality"

	1. Navigate to the mail page.
	1. Search for the email.
	1. Click on the reset password link.
	1. Switch to the iframe.
	1. Ctrl + Click on the reset password button to open the reset password form in a new tab.

#### ***ValidateMail***

--- 

This private method is used in [ResetPasswordESS](#resetpasswordess) method to validate the mail while entering the email to reset password.

=== "Method Signature"

	```csharp
	private void ValidateMail()
	```
=== "Functionality"

	1. Uses a while loop to implement a retry mechanism (5 retries).
	1. Simulate a arrow down key press in the email field.
	1. Check if the `SendVerificationCode` button is enabled.
	1. If the button is enabled, break from the while loop.
	1. If the button is disabled and retries haven't been exhausted, retry from step 2 again.
	1. If the button is disabled and retries have been exhausted, throws an exception saying "Email details not found".

#### **ResetPasswordESS**

---

This method is used to reset the password for the ESS user.

=== "Method Signature"

	```csharp
	public void ResetPasswordESS(string email, string pass, string orgName = null, string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `email` | `string` | The email of the user. |
	| `pass` | `string` | The new password to be set. |
	| `orgName` | `string` | The organization name in case the current candidate is onboarded in multiple organizations. |
	| `nodeName` | `string` | The name of the node to be shown on the Extent report. |

=== "Functionality"

	1. Open a New tab.
	1. Navigate to the mail page.
	1. Search for the email.
	1. Click on the reset password link.
	1. Switch to the iframe.
	1. Ctrl + Click on the reset password button to open the reset password form in a new tab.
	1. Enter the Email ID.
	1. Click on the Send Verification button.
	1. Check email for verification code.
	1. Enter the verification code in the verification code field and click on the verify button.
	1. Enter the new password and confirm password.
	1. If the parameter `orgName` is provided, go to the select organization page and select the organization.
	1. Wait until the url contains `dashboard`.

#### **SelectOrganization**

---

This method is used to select the organization in case the current candidate is onboarded in multiple organizations.

=== "Method Signature"

	```csharp
	public void SelectOrganization(string orgName)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `orgName` | `string` | The organization name to be selected. |

=== "Functionality"

	1. Navigate to the `SelectOrg_URL`.
	1. Select the organization based on `orgName`.
	1. Wait until the url contains `dashboard`.

