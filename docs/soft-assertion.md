# SoftAssertion

This class uses `Assert` class from NUnit framework (v3.13) to perform assertions but instead of failing the test immediately, it logs the assertion failures and continues with the test execution. The assertion failures are logged in the test report.

## **Normal Assertion**

---

```csharp
Assert.AreEqual("Actual", "Expected");
```
This Assertion throws an exception and stops the test execution if the actual and expected values are not equal.

## **Assertion using SoftAssert**

---

Pseudo-code for SoftAssert is as follows:

```
Assert expected and actual values
If assertion fails, log the failure to report and continue with the test execution
```

---

## Methods

### **AreEqual**

---

Asserts that two objects are equal. If the assertion fails, logs the failure to the report and continues with the test execution.

=== "Method Signature"

	```csharp
	public void AreEqual<T>(T expected, T actual, string message = null, string nodeName = null, IWebDriver driver = null, string parentNodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `expected` | `T` | The expected value. |
	| `actual` | `T` | The actual value. |
	| `message` | `string` | The message to log to the report if the assertion passes or fails. Defaults to `null`. |
	| `nodeName` | `string` | The name of the node for logging substeps. Defaults to `null`. |
	| `driver` | `IWebDriver` | The web driver instance. Defaults to `_driver`. Used in taking screenshot within the [`LogSubstep`](./reports-generation-class.md/#logsubstep) method invocation. |
	| `parentNodeName` | `string` | The name of the parent node. Defaults to `_test`. Used in logging substeps. |

=== "Functionality"

	- Uses `Assert.AreEqual` to compare the `expected` and `actual` values.
	- If the assertion fails or passes, logs the failure to the report using [`LogSubstep`](./reports-generation-class.md/#logsubstep) and adds the error to the errors list using [AddErrorMessage](#adderrormessage).
	- If the assertion fails, adds the error message to the list of errors along with the current stack frame (2-level deep) where the assertion has failed.

### **AreNotEqual**

---

Asserts that two objects are not equal. If the assertion fails, logs the failure to the report and continues with the test execution.

=== "Method Signature"

	```csharp
	public void AreNotEqual<T>(T notExpected, T actual, string message = null, string nodeName = null, IWebDriver driver = null, string parentNodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `notExpected` | `T` | The value that is not expected. |
	| `actual` | `T` | The actual value. |
	| `message` | `string` | The message to log to the report if the assertion passes or fails. Defaults to `null`. |
	| `nodeName` | `string` | The name of the node for logging substeps. Defaults to `null`. |
	| `driver` | `IWebDriver` | The web driver instance. Defaults to `_driver`. Used in taking screenshot within the [`LogSubstep`](./reports-generation-class.md/#logsubstep) method invocation. |
	| `parentNodeName` | `string` | The name of the parent node. Defaults to `_test`. Used in logging substeps. |

=== "Functionality"

	- Uses `Assert.AreNotEqual` to compare the `notExpected` and `actual` values.
	- If the assertion fails or passes, logs the failure to the report using [`LogSubstep`](./reports-generation-class.md/#logsubstep) and adds the error to the errors list using [AddErrorMessage](#adderrormessage).
	- If the assertion fails, adds the error message to the list of errors along with the current stack frame (2-level deep) where the assertion has failed.

### **Contains**

---

Asserts that a collection contains a specified element. If the assertion fails, logs the failure to the report and continues with the test execution.

=== "Method Signature"

	```csharp
	public void Contains<T>(T[] expected, T actual, string message = null, string nodeName = null, IWebDriver driver = null, string parentNodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `expected` | `T[]` | Array of expected values. |
	| `actual` | `T` | The actual value. |
	| `message` | `string` | The message to log to the report if the assertion passes or fails. Defaults to `null`. |
	| `nodeName` | `string` | The name of the node for logging substeps. Defaults to `null`. |
	| `driver` | `IWebDriver` | The web driver instance. Defaults to `_driver`. Used in taking screenshot within the [`LogSubstep`](./reports-generation-class.md/#logsubstep) method invocation. |
	| `parentNodeName` | `string` | The name of the parent node. Defaults to `_test`. Used in logging substeps. |

=== "Functionality"

	- Uses `Assert.Contains` to check if the `actual` value is present in the `expected` array.
	- If the assertion fails or passes, logs the failure to the report using [`LogSubstep`](./reports-generation-class.md/#logsubstep) and adds the error to the errors list using [AddErrorMessage](#adderrormessage).
	- If the assertion fails, adds the error message to the list of errors along with the current stack frame (2-level deep) where the assertion has failed.

### **IsTrue**

---

Asserts that a condition is `true`. If the assertion fails, logs the failure to the report and continues with the test execution.

=== "Method Signature"
	```csharp
	public void IsTrue(bool condition, string message = null, string nodeName = null, IWebDriver driver = null, string parentNodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `condition` | `bool` | The condition to evaluate. |
	| `message` | `string` | The message to log to the report if the assertion passes or fails. Defaults to `null`. |
	| `nodeName` | `string` | The name of the node for logging substeps. Defaults to `null`. |
	| `driver` | `IWebDriver` | The web driver instance. Defaults to `_driver`. Used in taking screenshot within the [`LogSubstep`](./reports-generation-class.md/#logsubstep) method invocation. |
	| `parentNodeName` | `string` | The name of the parent node. Defaults to `_test`. Used in logging substeps. |

=== "Functionality"

	- Uses `Assert.IsTrue` to check if the `condition` is `true`.
	- If the assertion fails or passes, logs the failure to the report using [`LogSubstep`](./reports-generation-class.md/#logsubstep) and adds the error to the errors list using [AddErrorMessage](#adderrormessage).
	- If the assertion fails, adds the error message to the list of errors along with the current stack frame (2-level deep) where the assertion has failed.

### **IsFalse**

---

Asserts that a condition is `false`. If the assertion fails, logs the failure to the report and continues with the test execution.

=== "Method Signature"

	```csharp
	public void IsFalse(bool condition, string message = null, string nodeName = null, IWebDriver driver = null, string parentNodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `condition` | `bool` | The condition to evaluate. |
	| `message` | `string` | The message to log to the report if the assertion passes or fails. Defaults to `null`. |
	| `nodeName` | `string` | The name of the node for logging substeps. Defaults to `null`. |
	| `driver` | `IWebDriver` | The web driver instance. Defaults to `_driver`. Used in taking screenshot within the [`LogSubstep`](./reports-generation-class.md/#logsubstep) method invocation. |
	| `parentNodeName` | `string` | The name of the parent node. Defaults to `_test`. Used in logging substeps. |

=== "Functionality"

	- Uses `Assert.IsFalse` to check if the `condition` is `false`.
	- If the assertion fails or passes, logs the failure to the report using [`LogSubstep`](./reports-generation-class.md/#logsubstep) and adds the error to the errors list using [AddErrorMessage](#adderrormessage).
	- If the assertion fails, adds the error message to the list of errors along with the current stack frame (2-level deep) where the assertion has failed.

### **AddErrorMessage**

---

Adds an error message to the list of errors in the `SoftAssertion` instance, along with the current stack frame where the error occurred.

=== "Method Signature"
	```csharp
	public void AddErrorMessage(string assertionErrorMessage, string customMessage = null, string stackFrameFailedLine = null)
	```

=== "Parameters"
	
	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `assertionErrorMessage` | `string` | The error message from the assertion. |
	| `customMessage` | `string` | An optional custom message to include in the error details. |
	| `stackFrameFailedLine` | `string` | The stack frame information of the failed line. |

=== "Functionality"

	- **Check Custom Message**:
		- If `customMessage` is not null or empty and is not already part of `assertionErrorMessage`, adds a combined message to the `errors` list in the format: `{customMessage} - {assertionErrorMessage} {stackFrameFailedLine}`.
	- **Add Assertion Error Message**:
		- If `customMessage` is null, empty, or already part of `assertionErrorMessage`, adds the message to the `errors` list in the format: `{assertionErrorMessage} {stackFrameFailedLine}`.

### **GetErrors**

---

Returns the list of errors in the `SoftAssertion` instance.

=== "Method Signature"

	```csharp
	public List<string> GetErrors()
	```

=== "Functionality"

	- Returns the list of errors.

=== "Usage"

	```csharp
	List<string> errors = assert.GetErrors();
	```

### ***GetStackFrameFailedLine***

---

Returns the current stack frame information of the failed line.

=== "Method Signature"

	```csharp
	private string GetStackFrameFailedLine()
	```

=== "Functionality"

	- **Get Stack Frame**: 	
		- Uses `new StackFrame(2, true)` to get the parent stack frame as the current stack frame would be in the `SoftAssertion` class.
		- Uses `new StackFrame(3, true)` to get the grandparent stack frame.
		- Returns the stack frame information as a string combining both the parent and grandparent stack frames.

=== "Returns"

	- Returns the stack frame information of the failed line.

=== "Usage"

	Used in all assertion methods to get the stack frame information of the failed line.
	```csharp
	string stackFrameFailedLine = GetStackFrameFailedLine();
	``

### **AssertAll**

---

Logs all the errors in the `SoftAssertion` instance to the report and clears the errors list.

=== "Method Signature"

	```csharp
	public void AssertAll(ExtentTest extentTest)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `extentTest` | `ExtentTest` | The ExtentTest instance where the errors should be logged. |

=== "Functionality"

	- **Set ExtentTest**:
		- Assigns the provided `extentTest` to the instance variable `this.extentTest`.
	- **Retrieve Errors**:
		- Calls [`GetErrors()`](#geterrors) to retrieve the list of errors.
	- **Check and Process Errors**:
		- If there are errors, iterates through the list and constructs a single message string from all errors:
			- Adds error to the message, ensuring that errors are indexed correctly.
			- If an error contains the index (formatted as ${index + 1}) ), the index is adjusted or removed accordingly.
	- **Log Errors**:
		- Calls [`LogError(extentTest, message)`](./reports-generation-class.md/#logerror) to log the constructed error message into the ExtentTest report using markup helpers for better formatting.
	- **Clear Errors**:
		- Clears the errors list.

## **Usage of Assertion Methods**

---

An `assert` object for `SoftAssert` class is created in the `ReportsGenerationClass` which will be inherited by `TestExecutionHelper` which in-turn is inherited by all test classes and this `assert` will be used to invoke the `SoftAssert` methods.

=== "AreEqual"
	
	```csharp
	public class TestClass : TestExecutionHelper
	{
		[Test]
		public void TestMethod()
		{
			assert.AreEqual("Actual", "Expected"));
		}

		[CleanUp]
		public void TestCleanup()
		{
			assert.AssertAll(GetExtentTest());
		}
	}
	```

=== "IsTrue"
	
	```csharp
	public class TestClass : TestExecutionHelper
	{
		[Test]
		public void TestMethod()
		{
			assert.IsTrue(true);
		}

		[CleanUp]
		public void TestCleanup()
		{
			assert.AssertAll(GetExtentTest());
		}
	}
	```

=== "AddErrorMessage"
	
	```csharp
	public class TestClass : TestExecutionHelper
	{
		[Test]
		public void TestMethod()
		{
			assert.AddErrorMessage("Error Message", "Custom Message");
		}

		[CleanUp]
		public void TestCleanup()
		{
			assert.AssertAll(GetExtentTest());
		}
	}
	```
