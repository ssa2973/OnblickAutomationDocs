# MailhogPage

The `MailhogPage` class contains all the locators and methods necessary to interact with the Mailhog page. Mailhog is an email testing tool for developers. It captures all the emails sent from the application and displays them in a web interface. The `MailhogPage` class is used to interact with the Mailhog web interface to verify that emails are being sent correctly. As the UI can take some time to load, the [`GetShowHeaders`](#getshowheaders) and [`GetHideHeaders`](#gethideheaders) methods are used after opening a mail to ensure that the mail body is loaded before proceeding with further actions.

## Members

### **Locators**

---

The locators used in the `MailhogPage` class aren't disclosed here, you can go through the `MailhogPage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`).

### **Methods**

---

There are several methods in the `MailhogPage` class that are used to interact with the Mailhog page. We shall only see the methods that are used often and not every method.

#### **GetShowHeaders**

---

The `GetShowHeaders` method is used to scroll to and click on an element identified as `showHeaders`. This method ensures that the element is brought into view before performing the click action.

=== "Method Signature"

	```csharp
	public void GetShowHeaders()
	```

=== "Functionality"

	1. **Scroll to Element**: Scroll to the `showHeaders` element to bring it into view.
	1. **Click on Element**: Click on the `showHeaders` element to display the email headers.

=== "Example Usage"

	```csharp
	MailhogPage mailhogPage = new MailhogPage();
	mailhogPage.GetShowHeaders();
	```

#### **GetHideHeaders**

---

The `GetHideHeaders` method is used to scroll to and click on an element identified as `hideHeaders`. This method ensures that the element is brought into view before performing the click action.

=== "Method Signature"

	```csharp
	public void GetHideHeaders()
	```

=== "Functionality"

	1. **Scroll to Element**: Scroll to the `hideHeaders` element to bring it into view.
	1. **Click on Element**: Click on the `hideHeaders` element to hide the email headers.

=== "Example Usage"

	```csharp
	MailhogPage mailhogPage = new MailhogPage();
	mailhogPage.GetHideHeaders();
	```

#### **GetIFrame**

---

The `GetIFrame` method is used to interact with and switch to an `iframe` inside a mail in mailhog page. It utilizes both [`GetShowHeaders`](#getshowheaders) and [`GetHideHeaders`](#gethideheaders) to ensure that the iframe is loaded properly before switching to it.

=== "Method Signature"

	```csharp
	public void GetIFrame()
	```

=== "Functionality"

	1. **Get Show Headers**: Call the `GetShowHeaders` method to ensure the mail body is loaded.
	1. **Get Hide Headers**: Call the `GetHideHeaders` method to ensure the mail body is loaded.
	1. **Switch to IFrame**: Switch to the `iframe` containing the mail body.

=== "Example Usage"

	```csharp
	MailhogPage mailhogPage = new MailhogPage();
	mailhogPage.GetIFrame();
	```

#### **Search**

--- 

The `Search` method is used to search for an email in the Mailhog page. It takes the email id as a parameter and searches for that it.

=== "Method Signature"

	```csharp
	public void Search(string mail)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `mail` | `string` | The email id to be searched. |

=== "Functionality"

	1. **Enter Email**: Enter the email id in the search bar.
	1. **Click Enter**: Click on the enter button to search for the email.

=== "Example Usage"

	```csharp
	MailhogPage mailhogPage = new MailhogPage();
	mailhogPage.Search("abc123@mail.com");
	```
