# MaildropPage

The `MaildropPage` class contains all the locators and methods necessary to interact with the Maildrop page of the application. This was created when we couldn't find an alternative for mailinator when it wasn't working but then we found [`Alternative Mailinator Domains`](./mailinator-page.md/#getrandommailinatordomain) so this class isn't used as of now.

## Members

### **Locators**

---

The locators used in the `MaildropPage` class aren't disclosed here, you can go through the `MaildropPage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`).

### **Methods**

---

There are only a few methods in the `MaildropPage` class that are used to interact with the Maildrop page.

#### **GetIFrame**

---

The `GetIFrame` method is used to switch to the iframe element on the Maildrop page. This method is used to interact with the email content displayed within the iframe.

=== "Method Signature"

	```csharp
	public void GetIFrame()
	```

=== "Functionality"

	- Switch to the iframe element on the Maildrop page.
	
=== "Example Usage"

	```csharp
	MaildropPage maildropPage = new MaildropPage();
	maildropPage.GetIFrame();
	```

#### **Search**

--- 

The `Search` method is used to search for an email in the Maildrop page. This method is used to filter emails based on the search criteria provided.

=== "Method Signature"

	```csharp
	public void Search(string email)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `email` | `string` | The email address to search for in the Maildrop page. |

=== "Functionality"

	1. Enter the email address in the search field.
	1. Click the search button to filter emails based on the search criteria.

=== "Example Usage"

	```csharp
	MaildropPage maildropPage = new MaildropPage();
	maildropPage.Search("abc123@mail.com");
	```