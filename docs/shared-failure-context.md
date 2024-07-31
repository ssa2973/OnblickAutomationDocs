# SharedFailureContext

The shared failure context allows different failure handlers to share information, such as error messages.

Below are the methods in `SharedFailureContext`:

## Methods

### **InitializeExceptionDetails**

---

Intializes the exception details in the shared failure context. It is used in [`ExecuteStep`](./testexecution-helper.md/#executestep) method in the catch block to initialize exception details after an exception was thrown.

=== "Method Signature"
	```csharp
	public static void InitializeExceptionDetails(Exception ex)
	```
=== "Parameters"
	
	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `ex` | `Exception` | The exception that was thrown. |

=== "Functionality"

	1. **Capture Method Name**:
		- Retrieves the name of the method where the exception was thrown using `TestContext.CurrentContext.Test.MethodName`.
		- Assigns the method name to the `FailedMethodName` field.
	1. **Extract Exception Message**:
		- Extracts the message from the exception `ex`.
		- Assigns the message to the `ExceptionMessage` field.
	1. **Process Stack Trace**:
		- Processes the stack trace of the exception using the [`GetStacktraceFailedLines`](#getstacktracefailedlines) method.
		- Assigns the processed stack trace to the `StackTrace` field.

=== "Usage"
	Used in the catch block of the [`ExecuteStep`](./testexecution-helper.md/#executestep) and [`ExecuteStepAndSuppress`](./testexecution-helper.md/#executestepandsuppress) methods and also in [`CustomRetryAttribute`](./attribute-extensions.md/#customretryattribute) to initialize the exception details in the shared failure context.
	```csharp
	SharedFailureContext.InitializeExceptionDetails(ex);
	```

### **ResetExceptionDetails**

---

Resets the exception details in the shared failure context. It is used in [`ExecuteStepAndSuppress`](./testexecution-helper.md/#executestepandsuppress) method in the finally block to reset exception details after the step has been executed.

=== "Method Signature"

	```csharp
	public static void ResetExceptionDetails()
	```
=== "Functionality"

	1. **Reset Method Name**:
		- Resets the `FailedMethodName` field to `null`.
	1. **Reset Exception Message**:
		- Resets the `ExceptionMessage` field to `null`.
	1. **Reset Stack Trace**:
		- Resets the `StackTrace` field to `null`.

=== "Usage"

	Used in the catch block of the [`ExecuteStepAndSuppress`](./testexecution-helper.md/#executestepandsuppress) method and also in `CleanUp` of some tests that use the `TestCaseSourceAttribute` to reset the exception details in the shared failure context.
	```csharp
	SharedFailureContext.ResetExceptionDetails();
	```

### **GetStacktraceFailedLines**

---

Processes the stack trace of the exception to extract the failed lines. It is used in the [`InitializeExceptionDetails`](#initializeexceptiondetails) method.

=== "Method Signature"

	```csharp
	public static string GetStacktraceFailedLines(string stackTrace)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `stackTrace` | `string` | The stack trace of the exception. |

=== "Functionality"

	1. **Split Stack Trace**:
		- Splits the input `stackTrace` string into individual lines using `\n` as the delimiter.
		- Stores the resulting lines in an array `lines`.
	1. **Initialize Updated Stacktrace**:
		- Initializes an empty string `updatedStacktrace` to store the processed stack trace lines.
	1. **Process Each Line**:
		- Iterates through each line in the `lines` array.
		- For each line, uses a regular expression to match the file name and line number.
		- Regex Pattern: `@"(?<file>[^\\]+\.cs):line (?<line>\d+)"`
		- Match Groups:
			- `file`: Captures the file name ending with `.cs`.
			- `line`: Captures the line number where the failure occurred.
	1. **Update Stacktrace**:
		- If a match is found, extracts the file name and line number.
		- Appends the formatted failure information to `updatedStacktrace` using HTML <br> tags for line breaks.
	1. **Return Result**:
		- Returns the `updatedStacktrace` string containing the formatted failure information.

=== "Usage"

	Used in the [`InitializeExceptionDetails`](#initializeexceptiondetails) method to process the stack trace of the exception.
	```csharp
	StackTrace = SharedFailureContext.GetStacktraceFailedLines(stackTrace);
	```
