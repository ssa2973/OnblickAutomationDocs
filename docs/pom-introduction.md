# Page Object Model

## **Introduction**

Page Object Model is a design pattern which has become popular in test automation for enhancing test maintenance and reducing code duplication. A page object is an object-oriented class that serves as an interface to a page of your application. 

## **Benefits of Page Object Model**

1. **Code Reusability**: Page Object Model allows you to write your tests in a more modular way, which means that you can reuse the same page object in multiple tests. This reduces code duplication and makes your tests easier to maintain.
1. **Code Maintainability**: Page Object Model makes your tests more maintainable because it separates the test logic from the page-specific logic. This means that if the page changes, you only need to update the page object, rather than updating all of your tests.
1. **Readability**: Page Object Model makes your tests more readable because it encapsulates the page-specific logic in a separate class. This makes it easier to understand what the test is doing, and makes it easier to write new tests.
1. **Reduced Code Duplication**: Page Object Model reduces code duplication by encapsulating the page-specific logic in a separate class. This means that you only need to write the page-specific logic once, rather than duplicating it in multiple tests.
1. **Improved Test Stability**: Page Object Model improves test stability by encapsulating the page-specific logic in a separate class. This means that if the page changes, you only need to update the page object, rather than updating all of your tests.

## **Page Object Model in Selenium**

In Selenium, Page Object Model is implemented by creating a separate class for each page of your application. Each page object class contains the page-specific logic, such as finding elements on the page and interacting with them. The test logic is then written in separate test classes, which use the page object classes to interact with the pages of the application.

## Example

In this example, we will create a page object class for the Google search page. The page object class will contain methods for interacting with the search page, such as entering a search query and clicking the search button. We will then write a test class that uses the page object class to perform a search on the Google search page.

=== "Page Object Class"

	```csharp
	using OpenQA.Selenium;
	using OpenQA.Selenium.Support.UI;

	namespace PageObjectModel
	{
		public class GoogleSearchPage
		{
			private IWebDriver driver;
			private By searchBox = By.Name("q");
			private By searchButton = By.Name("btnK");

			public GoogleSearchPage(IWebDriver driver)
			{
				this.driver = driver;
			}

			public void EnterSearchQuery(string query)
			{
				driver.FindElement(searchBox).SendKeys(query);
			}

			public void ClickSearchButton()
			{
				driver.FindElement(searchButton).Click();
			}

			public void WaitForSearchResults()
			{
				WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
				wait.Until(ExpectedConditions.ElementIsVisible(By.Id("result-stats")));
			}
		}
	}
	```

=== "Test Class"

	```csharp
	using OpenQA.Selenium;
	using OpenQA.Selenium.Chrome;
	using OpenQA.Selenium.Support.UI;
	using System;

	namespace PageObjectModel
	{
		[TestFixture]
		public class GoogleSearch
		{
			[SetUp]
			public void SetUp()
			{
				IWebDriver driver = new ChromeDriver();
				driver.Navigate().GoToUrl("https://www.google.com");
			}

			[Test]
			public void GoogleSearch_Test()
			{
				GoogleSearchPage searchPage = new GoogleSearchPage(driver);
				searchPage.EnterSearchQuery("Selenium");
				searchPage.ClickSearchButton();
				searchPage.WaitForSearchResults();
			}

			[CleanUp]
			public void CleanUp()
			{
				driver.Quit();
			}
		}
	}
	```

=== "Explanation"

	1. The `GoogleSearchPage` class is a page object class that represents the Google search page.
	1. The class has a constructor that takes an `IWebDriver` object as a parameter. This allows the page object class to interact with the browser.
	1. The class has methods for interacting with the search page, such as entering a search query, clicking the search button, and waiting for the search results to load.
	1. The `searchBox` and `searchButton` fields are `By` objects that represent the search box and search button elements on the page.
	1. The `EnterSearchQuery` method enters a search query into the search box.
	1. The `ClickSearchButton` method clicks the search button.
	1. The `WaitForSearchResults` method waits for the search results to load by waiting for the `result-stats` element to be visible.
	1. The `GoogleSearch` class is a test class that uses the `GoogleSearchPage` class to perform a search on the Google search page.
	1. The `SetUp` method creates a new `ChromeDriver` instance and navigates to the Google search page.
	1. The `GoogleSearch_Test` method creates a new `GoogleSearchPage` instance and performs a search for "Selenium".
	1. The `CleanUp` method quits the browser after the test has finished running.
