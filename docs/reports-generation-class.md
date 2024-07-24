# ReportsGenerationClass

This abstract class is used to generate the test reports, it is inherited by [`TestExecutionHelper`](./testexecution-helper.md). It uses the `ExtentReports` library to generate the reports. The reports are generated in the `Reports` folder in the project directory.

Below are the methods in the `ReportsGenerationClass` used to generate the reports:

## Members

### SetExtentTest

Sets the name for the current test instance - `ExtentTest` in the current `ExtentReport` instance.

=== "Method Signature"

	```csharp
	public static void SetExtentTest(string name)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `name` | `string` | The name of the test instance. |

=== "Functionality"

	1. **Set Test Name**:
		- Sets the name of the current test instance in the report to the provided `name`.

### GetExtentTest

Returns the instance of the `ExtentTest`.

=== "Method Signature"

	```csharp
	public static ExtentTest GetExtentTest()
	```
=== "Returns"

	`ExtentTest`: The instance of the `ExtentTest`.

=== "Funtionality"

	1. **Return Test Instance**:
		- Returns the `_test` field, which is an instance of `ExtentTest`.

### GetExtentReport

Returns the instance of the `ExtentReport`.

=== "Method Signature"

	```csharp
	public static ExtentReports GetExtentReport()
	```
=== "Returns"

	`ExtentReports`: The instance of the `ExtentReports`.

=== "Functionality"

	1. **Return Report Instance**:
		- Returns the `_extent` field, which is an instance of `ExtentReports`.

### GetDrivers

Returns the list of driver instances of `WebDriver` for the current test.

=== "Method Signature"

	```csharp
	public static List<IWebDriver> GetDrivers()
	```
=== "Returns"

	`List<IWebDriver>`: The list of driver instances.

=== "Functionality"

	1. **Return Drivers List**:
		- Returns the `drivers` list, which contains instances of `IWebDriver`.

### GetMethodByName

Gets a `MethodInfo` instance of the method by its name. Used in [BeforeTest](#beforetest) when the test method has a `TestCaseSourceAttribute`

=== "Method Signature"

	```csharp
	public static MethodInfo GetMethodByName(string methodName)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `methodName` | `string` | The name of the method to retrieve. |

=== "Returns"

	`MethodInfo`: The `MethodInfo` object representing the method, or `null` if the method is not found.

=== "Functionality"

	1. Get Executing Assembly:
		- Retrieves the currently executing assembly using `Assembly.GetExecutingAssembly()`.
	1. Get All Types:
		- Gets all types defined in the executing assembly using `executingAssembly.GetTypes()`.
	1. Find Method by Name:
		- Iterates through each type to find a method with the specified name using `type.GetMethod(methodName)`.
		- If the method is found, returns the corresponding `MethodInfo` object.
	1. Return Null if Not Found:
		- If no method with the specified name is found, returns `null`.

### ExportFailedDetails

Exports the failed test details to the report and log the status accordingly when the test either fails or is skipped.

=== "Method Signature"

	```csharp
	public static void ExportFailedDetails()
	```
=== "Functionality"

	1. **Get Test Status**:
		- Retrieves the current test status from `TestContext.CurrentContext.Result.Outcome.Status`.
	1. **Handle Failed Tests**:
		- If the test status is `TestStatus.Failed`:
			- Captures the current date and time.
			- Generates a screenshot filename and captures a screenshot in base64 format.
			- Creates a node in the report for failed details and network calls.
			- Logs the failure details, including the method name, exception message, and stack trace.
			- Logs relevant network call messages.
			- Adds the screenshot and the URL before failure to the report.
	1. **Handle Skipped Tests**:
		- If the test status is `TestStatus.Skipped`:
			- Creates a node in the report for skipped details.
			- Logs the reason for skipping, including the test name and exception message.

### ResetSubsteps

Resets or clears the substeps dictionary in the report.

=== "Method Signature"

	```csharp
	public static void ResetSubsteps()
	```
=== "Functionality"

	1. **Clear Substeps**:
		- Clears the `_substepNodes` dictionary.
	1. **Clear Substep Count**:
		- Clears the `_substepCounts` dictionary.

### Flush

Writes/updates the test information of your reporter to the destination type.

=== "Method Signature"

	```csharp
	public static void Flush()
	```
=== "Funtionality"

	1. **Flush Report**:
		- Calls `_extent.Flush()` to write/update the test information of the reporter to the destination type.

### SetDriver

Sets the driver instance of `WebDriver` for the current test and add the current driver to the list of drivers in case of multiple driver instances for a single test.

=== "Method Signature"

	```csharp
	public static IWebDriver SetDriver(IWebDriver driver)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | `IWebDriver` | The web driver instance to be set. |

=== "Returns"

	`IWebDriver`: The updated web driver instance.

=== "Functionality"

	1. **Set Current Driver**:
		- Assigns the provided `driver` to the `_driver` field.
	1. **Add to Drivers List**:
		- Adds `_driver` to the `drivers` list.
	1. **Return Driver**:
		- Returns the updated `_driver` instance.

### SetUp

Uses `OneTimeSetUp` attribute which runs this method once before all test methods in a test class. And this method adds all the necessary information of the current tests to the report.

=== "Method Signature"

	```csharp
	[OneTimeSetUp]
	protected void SetUp()
	```
=== "Functionality"

	1. **Initialize Web Drivers**:
		- Initializes `drivers` with a list containing `_driver`.
	1. **Set Trigger Source Information**:
		- Constructs `triggerSourceText` using the current test name.
		- Retrieves `triggerSource` from the Environment.
		- Adds system information to the extent report based on the value of triggerSource:
			- "Manual" if `triggerSource` is "MANUAL".
			- "Hosted Agent Pipeline" if `triggerSource` is "PIPELINE".
			- "Unknown" if `triggerSource` is null or empty.
	1. **Set Test Environment Information**:
		- Adds system information to the extent report about the test environment using `Environment.Name` and `URLs.Instance.Login_URL`.

### BeforeTest

Uses `OneTimeSetUp` attribute which runs this method once before all test methods in a test class. And this method handles the creation of a new test instance in the report along with output to console saying `Started Test: <TestMethodName> at <CurrentDateTime>` or `Retrying Test(s) at <CurrentDateTime>`

=== "Method Signature"

	```csharp
	[OneTimeSetUp]
	protected void BeforeTest()
	```

=== "Functionality"

	1. **Set Test Name**:
		- Creates a new test instance in the report using `ExtentTest` and sets the test name to the current test method name (unless the test has a TestCaseSourceAttribute, in which case it uses the SetExtentTest method to set a custom name for each test case).
		- Logs the start/retry of the test with the test name and start time to the console.
		- Assigns the test instance to the `_test` field.

### AfterTest

Uses `OneTimeTearDown` attribute which runs this method once after all test methods in a test class. And this method handles the cleaning up of resources along with output to console saying `Ended Test: <TestMethodName> at <CurrentDateTime> with status <TestStatus>, ran for duration : <TestDuration>`

=== "Method Signature"

	```csharp
	[OneTimeTearDown]
	protected void AfterTest()
	```

=== "Functionality"

	1. **Get Test Status**: 	
		- Retrieves the test status from the `TestContext.CurrentContext.Result.Outcome.Status` property.
		- If the test status is `Skipped`, logs the test status and duration.
		- If the test status is `Failed`, logs the test status, duration, and exception message.
		- If the test status is `Passed`, logs the test status and duration.
	1. [**Export Failed Details**](#exportfaileddetails):
		- Exports the failed test details to the report and logs the status accordingly when Test has either `Failed` or `Skipped`.
	1. **Reset/Clean Up Resources**:
		- Calls `ResetSubsteps` to clear the substeps dictionary in the current report.
		- Calls `Flush` to write/update the test information of the reporter to the destination type.
		- Closes and quits all the driver instances in the current test and clears the list of drivers.
		- Clears the list of errors in the [`SoftAssertion`](./soft-assertion.md) instance.
		- Logs the end of the test with the test status, duration, and end time to the console.

### Capture

Captures the screenshot of the current page and adds it to the report in base64 format.

=== "Method Signature"

	```csharp
	public static void Capture(IWebDriver driver, string screenShotName, string today)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | `IWebDriver` | The web driver instance. |
	| `screenShotName` | `string` | The name of the screenshot. |
	| `today` | `string` | The current date. |

=== "Returns"

	`string`: base64 string of the screenshot.

=== "Functionality"

	1. **Capture Screenshot**:
		- Captures a screenshot of the current page using `driver.TakeScreenshot()`.
	1. **Save Screenshot**:
		- Saves the screenshot to the `Reports` folder with a subdirectory from `Report today` the filename format `screenShotName.png`.
	1. **Return Screenshot Path**:
		- Returns the path of the saved screenshot.

### LogReport

Logs the message to the report with status Pass. Will be deprecated in a future version.

=== "Method Signature"

	```csharp
	public void LogReport(string message)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `message` | `string` | The message to log. |

=== "Functionality"

	1. **Log Message**:
		- Logs the message to the report with status `Pass`.


### LogInfo

Logs the message to the report with status Info. Will be deprecated a in a future version.

=== "Method Signature"

	```csharp
	public void LogInfo(string message)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `message` | `string` | The message to log. |

=== "Functionality"

	1. **Log Message**:
		- Logs the message to the report with status `Info`.


### LogError

Logs the error messages from [SoftAssertion](./soft-assertion.md) to the console and to the report in a markup helper.

=== "Method Signature"

	```csharp
	public void LogError(ExtentTest extentTest, string errorMessage)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `extentTest` | `ExtentTest` | The extent test instance to log the error message. |
	| `errorMessage` | `string` | The error message to log. |

=== "Functionality"

	1. **Log Error Message**:
		- Logs the error message to the console using `Console.WriteLine`.
	1. **Log Error to Report**:
		1.	**Markup Helper**:
			- Uses `MarkupHelper.CreateCodeBlock` to create a code block with the error message(s).
		1. **Assertion Failures Node**:
			- Creates a new node in `ExtentTest` instance with the name "Assertion Failures".
			- Attaches the `MarkupHelper` to the "Assertion Failures" node and shows the failures in `Status.Info`.

### GetOrCreateNode

Retrieves an existing `ExtentTest` node by name or creates a new one as a child of the specified parent node if it does not exist.

=== "Method Signature"

	```csharp
	private static ExtentTest GetOrCreateNode(string nodeName, ExtentTest parentNode)
	```
=== "Paramters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the node to retrieve or create. |
	| `parentNode` | `ExtentTest` | The parent node for the new node. |

=== "Returns"

	`ExtentTest`: The existing or newly created `ExtentTest` node.

=== "Functionality"

	1. **Check for Existing Node**:
		- Checks if `_substepNodes` contains an entry for `nodeName`.
	1. **Return Existing Node**:
		- If an entry exists, returns the existing `ExtentTest` node from `_substepNodes`.
	1. **Create New Node**:
		- If no entry exists, creates a new `ExtentTest` node as a child of `parentNode` using `parentNode.CreateNode(nodeName)`.
		- Adds the newly created node to `_substepNodes`.
	1. **Return New Node**:
		- Returns the newly created `ExtentTest` node.

### LogSubstep

The `LogSubstep` method logs details about a substep in a test to the specified node, capturing a screenshot if the substep fails.

=== "Method Signature"

	```csharp
	public void LogSubstep(string nodeName, string stepDetails, Status stepStatus? = null, string ssTitle = null, IWebDriver driver = null, string parentNodeName = null)
	```
=== "Paramters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the substep node. |
	| `stepDetails` | `string` | A description of the substep. |
	| `stepStatus` | `Status?` | The status of the substep. Default is `Status.Pass`. |
	| `ssTitle` | `string` | The title for the screenshot. |
	| `driver` | `IWebDriver` | The web driver instance. Default is `_driver`. |
	| `parentNodeName` | `string` | The name of the parent node. Default is `_test`. |

=== "Functionality"

	1. **Node and Parent Node Handling**:
		- Determines the parent node (either `_test` or `parentNodeName`).
		- Retrieves or creates the substep node (`nodeName`).
	1. **Substep Count Management**:
		- Initializes or increments the substep count for `nodeName`.
	1. **Logging**:
		- Logs the substep details with the status and a step label (e.g., "Step - X: ").
	1. **Screenshot Capture**:
		- If the substep status is neither `Pass` nor `Skip`, captures a screenshot using `driver` and adds it to the log entry.

This method provides systematic logging of substeps, ensuring each is recorded with specific details and an optional screenshot on failure.

### GetReportPath

The `GetReportPath` method generates a path for a report to be saved, ensuring necessary directories are created.

=== "Method Signature"

	```csharp
	public static string GetReportPath()
	```
=== "Returns"

	`string`: The current report path in the format `\\Reports\\Report dd_MM_yyyy\\ExtentReport - d_MMM_yy - H_mm.html`.

=== "Functionality"
	
	1. **Retrieve Current Directory**:
		- Gets the current directory using `Directory.GetCurrentDirectory()`.
	
	1. **Determine Project Path**:
		- Constructs the project path by navigating up three levels from the current directory.
	
	1. **Create Report Folder**:
		- Constructs the path for the `Reports` folder and ensures it is created using `Directory.CreateDirectory()`.
	
	1. **Create Date-Specific Report Folder**:
		- Constructs a date-specific folder path within the `Reports` folder and ensures it is created.
	
	1. **Generate Report Path**:
		- Constructs the report file path with a timestamp, ensuring it follows the format `ExtentReport - d_MMM_yy - H_mm.html`.
	
	1. **Return Report Path**:
		- Returns the constructed report path.

### AssignAuthor

The `AssignAuthor` method assigns the author name to the current test case.

=== "Method Signature"

	```csharp
	public void AssignAuthor(string authorName)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `authorName` | `string` | The author of the current test. |

=== "Functionality"

	1. **Assign Author**:
		- Assigns the provided author name to the current test using `_test.AssignAuthor(authorName)`.

### SwitchBrowser

The `SwitchBrowser` method switches the browser window to the specified window handle using webdriver instance in case of multiple webdriver instances.

=== "Method Signature"

	```csharp
	public void SwitchBrowser(IWebDriver driver)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | `IWebDriver` | The driver to switch to. |

=== "Functionality"

	1. **Switch Browser**:
		- Uses `driver.SwitchTo().Window(driver.CurrentWindowHandle)` to switch to the specified browser window.

### GetNetworkCalls

The `GetNetworkCalls` method retrieves and processes browser log entries, logging any failed network calls that meet specific criteria.

=== "Method Signature"

	```csharp
	protected void GetNetworkCalls(string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the node for logging substeps. Default is `null`. |

=== "Functionality"

	1. **Retrieve Browser Logs**:
		- Retrieves the browser logs using `_driver.Manage().Logs.GetLog(LogType.Browser)`.
	
	1. **Process and Filter Logs**:
		- Iterates through each log entry.
		- Checks if the log message contains the word "Failed" and does not contain "mailhog" or "help.onblick".
	
	1. **Log Relevant Entries**:
		- If a log entry meets the criteria, writes the error message to `TestContext.Progress` and logs it as a substep using `LogSubstep(nodeName, log.Message, Status.Info)`.

_Gets only failed network calls and is invoked when a test has failed._

### GetAllNetworkCalls

The `GetAllNetworkCalls` method retrieves and processes all browser log entries after ensuring there are no pending requests, logging any network calls that meet specific criteria.

=== "Method Signature"

	```csharp
	protected void GetAllNetworkCalls(string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the node for logging substeps. Default is `null`. |

=== "Functionality"

	1. **Wait for No Pending Requests**:
		- Calls `WaitForNoPendingRequests(_driver, 100)` to ensure there are no pending requests.
	
	1. **Retrieve Browser Logs**:
		- Retrieves the browser logs using `_driver.Manage().Logs.GetLog(LogType.Browser)`.
	
	1. **Process and Filter Logs**:
		- Iterates through each log entry.
		- Checks if the log message does not contain "mailhog" or "help.onblick".
	
	1. **Log Relevant Entries**:
		- If a log entry meets the criteria, writes the error message to `TestContext.Progress` and logs it as a substep using `LogSubstep(nodeName, log.Message)`.

_Note: This method is not used as of now as `WaitForNoPendingRequests(_driver,100)` doesn't work as expected in onblick application_
