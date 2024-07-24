# Writing Your First Test

## First Test

Now that we have our project set up, let's write our first test. We'll write a test that verifies that the Login function (`LoginPage.ValidLogin()`) works correctly. We'll write this test in a new file called `LoginTest.cs` in the `Test Plans` directory.

```csharp
using NUnit.Framework;
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using System;

namespace Test
{
	public class LoginTest
	{
		IWebDriver driver;

		[SetUp]
		public void Setup()
		{
			driver = new ChromeDriver();
			driver.Manage().Window.Maximize();
		}

		[Test]
		public void ValidLogin()
		{
			LoginPage loginPage = new LoginPage(driver);
			loginPage.ValidLogin(LoginCreds.Instance.HR_Email,LoginCreds.Instance.HR_Pwd);
			Assert.IsTrue(driver.Url.Contains("dashboard"));
		}

		[TearDown]
		public void TearDown()
		{
			driver.Quit();
		}
	}
}
```

This `ValidLogin()` method is already defined in the `LoginPage` class. We're using the [`Assert.IsTrue()`](./soft-assertion.md/#istrue) method to verify that the URL contains the string "dashboard" after a successful login. If the URL contains "dashboard", the test passes. If it doesn't, the test fails. And the [`LoginCreds`](./login-creds.md) class is also already defined in `TestData\LoginCredentials` folder. This class is used to store the login credentials for the test which are retrieved from `creds.json`.

The pseudo-code in `ValidLogin()` method is as follows:

=== "Pseudo Code"
```
Navigate to the login page
Enter the email and password
Click the login button
```

## Real-time Example for New Test

- First, create a new file in each Test Plans, Test Data, Page Object folders respectively
- Create a new test in the Test Plans folder corresponding to your current Test, let's name it `MyFirstTest.cs`.
- Create a new page object in the Page Object folder, let's name it `MyFirstPage.cs`. This file will contain all the locators and methods necessary to interact with the current page.
	- In case the number of methods is vast, you can separate the methods into a different file and create it in the `WebInteractions` folder. Let's name it `MyFirstInteractions.cs`.
	- In our project, the private By locator in the PageObject and the method that's used to access to the locator are written in the same line so as to be able to sort the locators easily.
- Create a new test data file in the Test Data folder, let's name it `MyFirstData.cs`. This file will contain all the data necessary for the test.

### Sample Code

=== "MyFirstTest.cs"
	```csharp
	using NUnit.Framework;
	using OpenQA.Selenium;
	using OpenQA.Selenium.Chrome;
	using System;

	namespace Test
	{
		public class MyFirstTest
		{
			IWebDriver driver;

			[SetUp]
			public void Setup()
			{
				driver = new ChromeDriver();
				driver.Manage().Window.Maximize();
			}

			[Test]
			public void MyFirstTest()
			{
				MyFirstPage myFirstPage = new MyFirstPage(driver);
				MyFirstInteractions myFirstInteractions = new MyFirstInteractions(driver);

				myFirstInteractions.MyFirstMethod(MyFirstData.Username, MyFirstData.Password);
				Assert.IsTrue(driver.Url.Contains("dashboard"));
			}

			[TearDown]
			public void TearDown()
			{
				driver.Quit();
			}
		}
	}
	```

=== "MyFirstPage.cs"
	```csharp
	using OpenQA.Selenium;
	using System;

	namespace PageObjects
	{
		public class MyFirstPage
		{
			IWebDriver driver;

			//Locators for your elements go here
			private By MyLocator = By.Id("myElement"); 
			public By MyLocatorId() { return MyLocator; }

			public MyFirstPage(IWebDriver driver)
			{
				this.driver = driver;
			}

			//if you do use PageFactory, use the elements from PageFactory here
			[FindsBy(How = How.Id, Using = "myElement")]
			public IWebElement MyElement
		}
	}
	```

=== "MyFirstInteractions.cs"
	```csharp
	using OpenQA.Selenium;
	using System;

	namespace WebInteractions
	{
		public class MyFirstInteractions
		{
			IWebDriver driver;

			public MyFirstInteractions(IWebDriver driver)
			{
				this.driver = driver;
			}

			public void MyFirstMethod(string data)
			{
				// Write your code here
			}
		}
	}
	```

=== "MyFirstData.cs"
	```csharp
	using System;

	namespace TestData
	{
		public class MyFirstData
		{
			//Test Data that you'll use in your Tests

			public static readonly string Username = "myUsername";
			public static readonly string Password = "myPassword";
		}
	}
	```