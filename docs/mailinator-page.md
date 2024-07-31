# MailinatorPage

The `MailinatorPage` class contains all the locators, and methods necessary to interact with the Mailinator page of the application. The Mailinator page is used to view and manage emails received by the application.

## Members

### **Locators**

---

The locators used in the `MailinatorPage` class aren't disclosed here, you can go through the `MailinatorPage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`).

### **Methods**

---

There are several methods in the `MailinatorPage` class that are used to interact with the Mailinator page. We shall only see the methods that are used often and not every method.

#### **GetRandomMailinatorDomain**

---

The `GetRandomMailinatorDomain` method generates a random email domain from a predefined list of Mailinator domains. This can be useful for generating temporary or disposable email addresses for testing purposes.

=== "Method Signature"

	```csharp
	public static string GetRandomMailinatorDomain()
	```
=== "Returns"

	`string`: A randomly selected Mailinator domain from the predefined list.

=== "Functionality"

	1. **Select Random Domain**: Randomly select a Mailinator domain from the predefined list.
	1. **Return Domain**: Return the selected domain as a string.

=== "Domain List"

	```csharp
	var allDomains = new string[]
    {
        "@binkmail.com",
        "@bobmail.info",
        "@chammy.info",
        "@devnullmail.com",
        "@mailinater.com",
        "@mailinator.net",
        "@notmailinator.com",
        "@reallymymail.com",
        "@safetymail.info",
        "@sendspamhere.com",
        "@sogetthis.com",
        "@spamhereplease.com",
        "@suremail.info",
        "@thisisnotmyrealemail.com",
        "@tradermail.info",
        "@veryrealemail.com",
        "@zippymail.info",
    };
	```

#### **GetIFrame**

---

The `GetIFrame` method is used to switch to the iframe containing the email content. This method is necessary to interact with the email content displayed within the iframe.

=== "Method Signature"

	```csharp
	public void GetIFrame()
	```

=== "Functionality"

	- Switch the driver context to the iframe containing the email content.

=== "Example Usage"

	```csharp
	MailinatorPage mailinatorPage = new MailinatorPage();
	mailinatorPage.GetIFrame();
	```

#### **Search**

---

The `Search` method is used to search for an email in the Mailinator page. It takes the email id as a parameter and searches for that email.

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
	MailinatorPage mailinatorPage = new MailinatorPage();
	mailinatorPage.Search("abc123@mail.com");
	```