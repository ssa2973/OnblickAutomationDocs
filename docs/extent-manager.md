# ExtentManager

The `ExtentManager` class is responsible for managing the creation and configuration of the Extent Reports instance used for generating test reports. It ensures that the reporting setup is initialized only once and provides access to the configured `ExtentReports` instance.


## **Class Definition**

---

```csharp
public class ExtentManager
```

## **Properties**

---

- ExtentReports extent: Static instance of `ExtentReports` used to generate and manage reports.

## **Methods**

---

=== "GetInstance"

	```csharp
	public static ExtentReports GetInstance()
	```

=== "Description"

	This method creates and returns a singleton instance of `ExtentReports`. If an instance of `ExtentReports` does not already exist, it initializes one and configures it with an `ExtentV3HtmlReporter`.

=== "Returns"

	- The configured `ExtentReports` instance.

=== "Details"

	1. HTML Reporter Configuration:
		- Theme: Dark
		- Timeline: Disabled
	1. Report Path: Retrieved using [`ReportsGenerationClass.GetReportPath()`](./reports-generation-class.md/#getreportpath).

=== "Usage Example"

	```csharp
	ExtentReports extent = ExtentManager.GetInstance();
	```

## **Notes**

---

- The singleton pattern is used to ensure that only one instance of ExtentReports is created and used throughout the test execution.
- The HTML reporter settings are configured to use a dark theme and disable the timeline feature.