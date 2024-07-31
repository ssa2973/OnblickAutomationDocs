# AttributeExtensions

`AttributeExtensions` is a library that provides a set of extension methods for working with NUnit attributes.

## Members

### **CustomRetryAttribute**

---

`CustomRetryAttribute` is an attribute that can be used to specify the number of times a test should be retried if it fails with a particular exception which contains `"The HTTP request to the remote WebDriver server for URL"` in the message.

#### Constructor

=== "CustomRetryAttribute"
	```csharp
	public CustomRetryAttribute(int tryCount)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `tryCount` | `int` | The number of times the test should be retried including the initial run. |

#### Methods

##### Wrap

Wraps a test method command and returns the result.

=== "Wrap"
	```csharp
	public TestCommand Wrap(TestCommand command)
	{
		return new RetryCommand(command, _tryCount);
	}
	```	
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `command` | `TestCommand` | The inner command to be executed. |


#### Nested Class: Retry Command

The `RetryCommand` class implements the logiv for retrying a test method.

##### Constructor

=== "RetryCommand"
	```csharp
	public RetryCommand(TestCommand innerCommand, int tryCount)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `innerCommand` | `TestCommand` | The inner command to be executed. |
	| `tryCount` | `int` | The number of times the test should be retried including the initial run. |

##### Execute Method

**Description**: Runs the test, saving a `TestResult` in the supplied `TestExecutionContext`. In case of retries, it will re-run the test after clearing drivers and reports.

=== "Execute"
	```csharp
	public override TestResult Execute(TestExecutionContext context)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `context` | `TestExecutionContext` | The current `TestExecutionContext`. |

=== "Returns"
	`TestResult` - The result of the test execution.


#### Usage

=== "Example 1"
	```csharp
	[Test]
	[CustomRetry(3)]
	public void TestMethod()
	{
		// Test code
	}
	```
=== "Example 2"
	```csharp
	[Test, CustomRetry(3)]
	public void TestMethod()
	{
		// Test code
	}
	```
_Note: Both examples apply the `Test` and `CustomRetry(3)` attributes to the `TestMethod`. The choice between the two styles is mostly a matter of personal preference or coding style guidelines_

### **IgnoreAssertionFailuresAttribute**

---

The `IgnoreAssertionFailuresAttribute` class is used to specify that a test should be marked as passed if it failed only due to soft assertion failures.

#### Methods

##### Wrap

Wraps a test method command and returns the result.

=== "Wrap"
	```csharp
	public TestCommand Wrap(TestCommand command)
	{
		return new IgnoreAssertionFailuresCommand(command);)
	}
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `command` | `TestCommand` | The inner command to be executed. |

#### Nested Class: Ignore Assertion Failures Command

The `IgnoreAssertionFailuresCommand` class implements the logic for ignoring assertion failures.

##### Constructor

=== "IgnoreAssertionFailuresCommand"
	```csharp
	public IgnoreAssertionFailuresCommand(TestCommand innerCommand)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `innerCommand` | `TestCommand` | The inner command to be executed. |

##### Execute Method

**Description**: Runs the test, saving a `TestResult` in the supplied `TestExecutionContext`. In case of test failure only due to assertion failures, it will mark the test as passed.

=== "Execute"
	```csharp
	public override TestResult Execute(TestExecutionContext context)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `context` | `TestExecutionContext` | The current `TestExecutionContext`. |

=== "Returns"
	`TestResult` - The result of the test execution.

#### Usage

=== "Example 1"
	```csharp
	[Test]
	[IgnoreAssertionFailures]
	public void TestMethod()
	{
		// Test code
	}
	```

=== "Example 2"
	```csharp
	[Test, IgnoreAssertionFailures]
	public void TestMethod()
	{
		// Test code
	}
	```
_Note: Both examples apply the `Test` and `IgnoreAssertionFailures` attributes to the `TestMethod`. The choice between the two styles is mostly a matter of personal preference or coding style guidelines_

---


