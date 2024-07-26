# Project Guidelines

Page Object Model in our current Project follows some guidelines and practices. These guidelines are created to ensure that the project is maintainable, scalable and readable.

## **Constructing Locators**

Below are the conventions to follow for writing locators in the project:

1. **Use ID, Name, CSS, XPath locators in the order of preference**:
	- ID is the most preferred locator followed by Name, CSS and XPath.
	- If ID is not available, use Name locator.
	- If Name locator is not available, use CSS locator.
	- If CSS locator is not available, use XPath locator.
	- But more often than not, in [Onblick 2.0](https://www.onblick.com){:target=_blank} ID, Class, CSS locators are dynamically generated. So it is better to use XPath locators.
1. **Use Relative XPath**:
	- Always use relative XPath instead of absolute XPath.
	- Avoid using absolute XPath as it is not reliable and breaks easily.
	- Use XPath axes like `following-sibling`, `preceding-sibling`, `parent`, `child`, `ancestor`, `descendant` etc. to create more reliable XPath.
	- Use `normalize-space`, `contains`, `starts-with`, `ends-with` functions in XPath to create more reliable XPath.

=== "Example"

	```csharp
	// Relative XPath
	By.XPath("//input[@id='username']")

	// Absolute XPath
	By.XPath("/html/body/div[1]/div[2]/div[3]/div[4]/input")
	```
## **Best Practices for Current Project**

1. **Use Page Object Model**:
	- Use Page Object Model to create a separate class for each page.
	- Define all the locators (and methods - optional) related to that page in that class.
1. **Use Page Factory**:
	- Use Page Factory to initialize the elements in the page class.
	- Use `FindsBy` annotation to define the locators in the page class.
	- Use `PageFactory.InitElements(driver, this)` to initialize the elements in the page class.
	- _Note: `PageFactory` was used in the current project in almost all page object classes. However, the more recent versions of Selenium do not support `PageFactory` so it is better to avoid using it in the new page object classes._

=== "Example"

	```csharp
	private readonly By Username = By.Id("username"); public By UsernameId() { return Username; }
	private readonly By Password = By.Id("password"); public By PasswordId() { return Password; }
	```

=== "Example of PageFactory"
	
	```csharp
	//Only in case you do end up using it, here is an example of how to use it:
	[FindsBy(How = How.Id, Using = "username")]
	private IWebElement Username

	[FindsBy(How = How.Id, Using = "password")]
	private IWebElement Password
	```
=== "PageObject Class"
	
	```csharp
	public class LoginPage
	{
		private readonly IWebDriver driver;

		private readonly By Username = By.Id("username"); public By UsernameId() { return Username; }
		private readonly By Password = By.Id("password"); public By PasswordId() { return Password; }

		public LoginPage(IWebDriver driver)
		{
			this.driver = driver;
			PageFactory.InitElements(driver, this);
		}

		[FindsBy(How = How.Id, Using = "username")]
		private IWebElement Username;

		[FindsBy(How = How.Id, Using = "password")]
		private IWebElement Password;

		public void Login(string username, string password)
		{
			Username.SendKeys(username);
			Password.SendKeys(password);
		}
	}
	```

