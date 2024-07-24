# ExtentManager

Below are the methods in the `ExtentManager` class used to manage the extent reports:

## Members

### GetInstance

Creates a new `HtmlReporter` instance, attaches it to the `ExtentReports` instance and returns the `ExtentReports` instance.

=== "Method Signature"

	```csharp
	public static ExtentReports GetInstance()
	```
=== "Returns"

	An `ExtentReports` instance.

=== "Usage"
	
	Used in [`ReportsGenerationClass`](./reports-generation-class.md) to get the `ExtentReports` instance.)
	```csharp
	ExtentReports extent = ExtentManager.GetInstance();
	```