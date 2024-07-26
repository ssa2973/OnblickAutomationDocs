# WebDriverExtensions

WebDriverExtensions is a collection of extensions for Selenium WebDriver. It provides a set of useful methods and classes to work with WebDriver.

## Methods

### **OpenNewTab**

The `OpenNewTab` method is an extension method that opens a new tab.

=== "Method Signature"
	```csharp
	public static void OpenNewTab(this IWebDriver driver)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |

=== "Functionality"

	1. **JavaScript Execution**: Executes a JavaScript script to open a new tab.
	1. **New Tab**: Opens a new tab in the browser.

=== "Usage"
	```csharp
	driver.OpenNewTab();
	```

---

### **UploadFile**

The `UploadFile` method is an extension method that uploads a file to a file input element.

=== "Method Signature"
	```csharp
	public static void UploadFile(this IWebDriver driver, string filePath)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |
	| `filePath` | string | The path to the file to upload. |

=== "Functionality"

	1. **Find Element**: Finds the file input element on the page.
	1. **Send Keys**: Sends the file path to the file input element.

=== "Usage"
	```csharp
	driver.UploadFile("C:\\path\\to\\file.txt");
	```

---

### **GetUserName**

The `GetUserName` method is an extension method that retrieves the username of the current user.

=== "Method Signature"
	```csharp
	public static string GetUserName(this IWebDriver driver)
	```

=== "Paramters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |

=== "Functionality"

	1. **Username**: Retrieves the username of the current user from the top right section of the page.

=== "Usage"
	
	To Get the username of the currently logged in user.
	```csharp
	string userName = driver.GetUserName();
	```
---

### **GetDesignation**

The `GetDesignation` method is an extension method that retrieves the designation of the current user.

=== "Method Signature"
	```csharp
	public static string GetDesignation(this IWebDriver driver)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |

=== "Functionality"

	1. **Designation**: Retrieves the designation of the current user from the top right part of the page.

=== "Usage"

	To Get the designation of the currently logged in user.
	```csharp
	string designation = driver.GetDesignation();
	```

---

### **GetCurrentRole**

The `GetCurrentRole` method is an extension method that retrieves the current role of the user.

=== "Method Signature"
	```csharp
	public static string GetCurrentRole(this IWebDriver driver)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |

=== "Functionality"

	1. **Role**: Retrieves the current role of the user from the top right part of the page.

=== "Usage"

	To Get the current role of the user.
	```csharp
	string role = driver.GetCurrentRole();
	```

---

### **GetOrgName**

The `GetOrgName` method is an extension method that retrieves the organization name of the user.

=== "Method Signature"
	```csharp
	public static string GetOrgName(this IWebDriver driver)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |

=== "Functionality"

	1. **Organization Name**: Retrieves the organization name of the user from the top left part of the page.

=== "Usage"

	To Get the organization name of the user.
	```csharp
	string orgName = driver.GetOrgName();
	```

---

### **GetCandidateProfileName**

The `GetCandidateProfileName` method is an extension method that retrieves the candidate profile name.

=== "Method Signature"
	```csharp
	public static string GetCandidateProfileName(this IWebDriver driver)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |

=== "Functionality"

	1. **Candidate Profile Name**: Retrieves the candidate profile name.

=== "Usage"

	To Get the candidate's name from the candidate profile.
	```csharp
	string candidateProfileName = driver.GetCandidateProfileName();
	```

---

### ***SetZoomLevel***

The `SetZoomLevel` method is an extension method that sets the zoom level of the browser.

=== "Method Signature"
	```csharp
	public static void SetZoomLevel(this IWebDriver driver, int zoomPercent)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |
	| `zoomPercent` | int | The zoom level percentage. |

=== "Functionality"

	1. **JavaScript Execution**: Executes a JavaScript script to set the zoom level.
	1. **Zoom Level**: Sets the zoom level of the browser to the specified percentage.
	1. **Zoom In/Out**: Increases or decreases the zoom level.


=== "Usage"
	```csharp
	driver.SetZoomLevel(150);
	```
_Note: Refrain from using this method for now as it's still a bit undeveloped._

---

### ***ClickByOffSetFromViewport***

The `ClickByOffSetFromViewport` method is an extension method that clicks on the webpage by providing the offset from the viewport.

=== "Method Signature"
	```csharp
	public static void ClickByOffSetFromViewport(this IWebDriver driver, Point point)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `driver` | IWebDriver | The WebDriver instance. |
	| `point` | Point | The offset from the viewport. |

=== "Functionality"

	1. **JavaScript Execution**: Executes a JavaScript script to click on the webpage.
	1. **Offset**: Clicks on the webpage at the specified offset from the viewport.

=== "Usage"
	```csharp
	driver.ClickByOffSetFromViewport(new Point(100, 100));
	```
_Note: Refrain from using this method for now as it's still a bit undeveloped._

---