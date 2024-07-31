# WorkforcePage

The `WorkforcePage` class contains all the enums, locators and methods necessary to interact with the Workforce page of the application. The Workforce page is used to manage the workforce of an organization, including adding, editing, and deleting employees.

## Members

### **Enums**

---

The `WorkforcePage` class contains the following enums:

#### **EmployeeType**

The `EmployeeType` enumeration represents different states or categories of an employee within the system. This enum is used to classify and manage employees based on their current employment status.

=== "Enum Members"

	| Member | Description |
	| ------ | ----------- |
	| `Active` | Represents an active employee. |
	| `NewHire` | Represents a new hire employee. |
	| `Terminated` | Represents a terminated employee. |

=== "Usage"

	This enum is used in multiple worforce methods to classify employees based on their current status.

	```csharp
	EmployeeType employeeType1 = EmployeeType.Active;
	EmployeeType employeeType2 = EmployeeType.NewHire;
	EmployeeType employeeType3 = EmployeeType.Terminated;
	```

### **Locators**

---

The locators used in the `WorkforcePage` class aren't disclosed here, you can go through the `WorkforcePage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`).

### **Methods**

---

The `WorkforcePage` class contains several methods that are used to interact with the Workforce page. Some of the methods are private and some are public, italicized methods are private methods.

#### **SearchEmployee**

---

The `SearchEmployee` method searches for an employee in the workforce based on their email and first name. It navigates to the appropriate workforce URL depending on the employee's status (`Active`, `NewHire`, or `Terminated`) and performs a search. If the employee is not found and the status is `Active`, it will attempt to search under `NewHire` status as well.

=== "Method Signature"

	```csharp
	public void SearchEmployee(string empMail, string empFirstName, EmployeeType? employeeType = null, string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empMail` | `string` | The email address of the employee to search for. |
	| `empFirstName` | `string` | The first name of the employee to search for. |
	| `employeeType` | `EmployeeType?` | The type of employee to search for (`Active`, `NewHire`, or `Terminated`). |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Navigate to the appropriate workforce URL based on the employee's status.
	1. Enter the email address of the employee in the search fields.
	1. Click the search button to find the employee.
	1. Wait until the employee is found with `empFirstName`.
	1. If the employee is not found and the status is `Active`, attempt to search under `NewHire` status as well.

=== "Example Usage"

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.SearchEmployee("john.doe@example.com", "John", EmployeeType.NewHire, "Search Workforce");
	```

#### ***SearchEmployee***

---

The `SearchEmployee` method searches for an employee in the workforce based on their email. It navigates to the appropriate workforce URL depending on the employee's status (`Active`, `NewHire`, or `Terminated`) and performs a search. This method is only for [`TryDeleteEmployee`], DO NOT use it anywhere else, as it's functionality will also be changed soon.

=== "Method Signature"

	```csharp
	public void SearchEmployee(string empMail, EmployeeType? employeeType = null, string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empMail` | `string` | The email address of the employee to search for. |
	| `employeeType` | `EmployeeType?` | The type of employee to search for (`Active`, `NewHire`, or `Terminated`). |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Navigate to the appropriate workforce URL based on the employee's status.
	1. Enter the email address of the employee in the search fields.
	1. Click the search button to find the employee.

=== "Example Usage"

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.SearchEmployee("john.doe@example.com", EmployeeType.NewHire, "Search Employee");
	```

#### **GoToEmployeeProfile**

---

The `GotoEmployeeProfile` method navigates to an employee's profile based on the provided [`OnboardDetails`](./onboard-page.md/#onboarddetails). It handles navigation through various conditions, including checking if the profile name matches, handling pop-ups, and searching for the employee. This method uses [`GetCandidateProfileName`](./webdriver-extensions.md/#getcandidateprofilename) and [`SearchEmployee`](#searchemployee) methods internally.

=== "Method Signature"

	```csharp
	public void GotoEmployeeProfile(OnboardDetails onboardDetails, EmployeeType? empType = null, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetails` | [`OnboardDetails`](./onboard-page.md/#onboarddetails) | The details of the employee to navigate to. |
	| `empType` | `EmployeeType?` | The type of employee to search for (`Active`, `NewHire`, or `Terminated`). |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Retrieve Candidate Profile Name: Retrieves the candidate profile name from the current page.
	1. Check Profile Name: Checks if the retrieved profile name contains the first and last name from onboardDetails.
	1. Navigate to Profile:
		- If the profile name is null or doesn't match, it navigates to the profile through a pop-up which comes after onboarding or by searching for the employee.
	1. Log Navigation: Logs the navigation to the employee profile to the report.

=== "Example Usage"

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.GotoEmployeeProfile(onboardDetails, EmployeeType.Active, "Navigate to Profile");
	```

#### ***Delete***

---

The `Delete` method handles the deletion of records based on the provided `EmployeeType` and locator. It performs different actions depending on whether the employee is `Active`/`NewHire` or `Terminated`. This method is an internal method used in [`DeleteEmployee`](#deleteemployee) and [`DeleteEmployees`](#deleteemployees) methods.

=== "Method Signature"

	```csharp
	private void Delete(EmployeeType employeeType, By Locator)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `employeeType` | `EmployeeType` | The type of employee to delete (`Active`, `NewHire`, or `Terminated`). |
	| `Locator` | `By` | The locator to identify the delete button for the employee. |

=== "Functionality"

	1. Click on the delete button based on the provided locator.
	1. Handle the deletion process based on the employee type (`Active`/`NewHire` or `Terminated`).

=== "Usage"

	This method is used internally in the `DeleteEmployee` and `DeleteEmployees` methods. This method is only intended for those 2 methods, **DO NOT** use it anywhere else.

#### **DeleteEmployee**

---

The `DeleteEmployee` method searches for an employee by email and first name and then deletes the employee record. It handles different actions based on the `EmployeeType`. This method uses the [`SearchEmployee`](#searchemployee), [`Delete`](#delete), and [`DeleteI9`](#deletei9) methods internally.

=== "Method Signature"

	```csharp
	public void DeleteEmployee(string empMail, string empFirstName, EmployeeType? employeeType = null, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empMail` | `string` | The email address of the employee to delete. |
	| `empFirstName` | `string` | The first name of the employee to delete. |
	| `employeeType` | `EmployeeType?` | The type of employee to delete (`Active`, `NewHire`, or `Terminated`). |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Determine Employee Type: If employeeType is not specified, it defaults to Active.
	1. Set Locators: Based on the employeeType, set the appropriate locators for employee actions and delete buttons.
	1. Search Employee: Use the SearchEmployee method to find the employee by email and first name.
	1. Delete Employee: Iterate through the located elements and delete the employee. Handle possible popups and exceptions.
		- One possibility for exception is where there's an I-9 for the current candidate, in which case delete directly isn't possible. So, I-9 is first deleted with [`DeleteI9`](#deletei9) method and then the candidate is deleted.
		- Another possiblity for exception is where the candidate has reporting candidates, in which case there's a confirmation popup to unlink the reporting candidates before deletion.

=== "Example Usage"

	This method should be the go to method to delete an employee. It handles all the necessary steps to delete an employee.

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.DeleteEmployee("john.doe@example.com", "John", EmployeeType.Terminated, "Delete");
	```

#### ***DeleteEmployees***

---

The DeleteEmployees method searches for multiple employee records by email and first name and deletes them. It handles different actions based on the EmployeeType. This method is designed for and used only in [`TryDeleteEmployee`](#trydeleteemployee) method, **DO NOT** use it anywhere else. This method uses the [`Delete`](#delete) and [`DeleteI9`](#deletei9) methods internally.

=== "Method Signature"

	```csharp
    public void DeleteEmployees(string empMail, string empFirstName, EmployeeType? employeeType = null, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empMail` | `string` | The email address of the employee to delete. |
	| `empFirstName` | `string` | The first name of the employee to delete. |
	| `employeeType` | `EmployeeType?` | The type of employee to delete (`Active`, `NewHire`, or `Terminated`). |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Determine Employee Type: If employeeType is not specified, it defaults to Active.
	1. Set Locators: Based on the employeeType, set the appropriate locators for employee actions and delete buttons.
	1. Locate and Delete Employees: Find all elements matching the locator and delete each employee, handling possible popups and exceptions.

=== "Usage"

	This method is used internally in the `TryDeleteEmployee` method. It is not intended for use outside of this context.

#### **TryDeleteEmployee**

---

The `TryDeleteEmployee` method attempts to delete an employee by email and first name from various employee categories. It first attempts to delete the employee from the `Terminated` category and then proceeds to check and delete the employee from the `Active` and `NewHire` categories if they exist. Exception handling ensures that any issues encountered during the deletion process are appropriately managed.

=== "Method Signature"

	```csharp
	public void TryDeleteEmployee(string empMail, string empFirstName, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empMail` | `string` | The email address of the employee to delete. |
	| `empFirstName` | `string` | The first name of the employee to delete. |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Search and Delete from `Terminated`: Search for the employee in the Terminated category and delete if found.
	1. Search and Delete from `Active` and `NewHire`: Search and delete the employee from the Active and NewHire categories if found. Handle exceptions that may occur during this process.
	1. Only Tries to Delete from any category if the candidate already exists and if not, handles any exceptions that may occur.

=== "Example Usage"

	This method is useful when you are onboarding a candidate and want to ensure that any existing records are deleted before proceeding.

	```csharp
	WorkforcePage workforcePage = new WorkforcePage(driver);
	workforcePage.TryDeleteEmployee("john.doe@example.com", "John", "Node1");
	```

#### **DeleteI9**

---

The `DeleteI9` method is used to delete an I-9 form for an employee specified by their first name. This method handles the navigation to the I-9 tab within the employee's profile and performs the necessary steps to delete the I-9 form, including handling any warnings and verifying element visibility and clickability.

=== "Method Signature"

	```csharp
	public void DeleteI9(string empFirstName, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empFirstName` | `string` | The first name of the employee whose I-9 form is to be deleted. |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Navigate to the I-9 tab within the employee's profile.
	1. Click the delete button to remove the I-9 form.
	1. Handle any warnings or confirmations that may appear during the deletion process.

=== "Usage"

	This method is designed for and used in only the [`DeleteEmployee`](#deleteemployee) method. It should not be used outside of this context.

#### **EnableESS**

---

The `EnableEss` method is used to enable the Employee Self-Service (ESS) feature. It waits for the ESS slider button to be visible, checks its current state, and enables it if it is not already enabled. The method then logs the action and validates that ESS is indeed enabled.

=== "Method Signature"

	```csharp
	public void EnableEss(string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Wait for the ESS slider button to be visible.
	1. Check the current state of the ESS slider.
	1. If the ESS slider is not enabled, click it to enable ESS.
	1. Log the action to the report and validate that ESS is enabled.

=== "Usage"

	This method is used to enable the Employee Self-Service feature in the application, assuming we're already on the candidate profile. If not use [`GoToEmployeeProfile`](#gotoemployeeprofile) first and then `EnableESS`.

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.EnableEss("Enable ESS");
	``

#### **DisableESS**

---

The `DisableEss` method is used to disable the Employee Self-Service (ESS) feature. It waits for the ESS slider button to be visible, checks its current state, and disables it if it is not already disabled. The method then logs the action and validates that ESS is indeed disabled.

=== "Method Signature"

	```csharp
	public void DisableEss(string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Wait for the ESS slider button to be visible.
	1. Check the current state of the ESS slider.
	1. If the ESS slider is enabled, click it to disable ESS.
	1. Log the action to the report and validate that ESS is disabled.

=== "Usage"

	This method is used to disable the Employee Self-Service feature in the application, assuming we're already on the candidate profile. If not use [`GoToEmployeeProfile`](#gotoemployeeprofile) first and then `DisableESS`.

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.DisableEss("Disable ESS");
	```
#### ***GetTextFromColumn***

---

The `GetTextFromColumn` method retrieves the text content of the first cell in a specified column of an HTML table, based on the header text provided. It identifies the column index using the header text, then extracts the text from the corresponding cell. This method is used in [`ValidateCandidateDetails`](#validatecandidatedetails) method

=== "Method Signature"

	```csharp
	public string GetTextFromColumn(string headerText)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `headerText` | `string` | The text of the column header to identify the column. |

=== "Returns"

	- The text content of the first cell in the specified column.

=== "Functionality"

	1. Identify the column index based on the provided header text.
	1. Retrieve the text content of the first cell in the identified column.

=== "Usage"

	This method is used internally in the `ValidateCandidateDetails` method to extract specific details from the candidate profile.

#### **ValidateCandidateDetails**

---

The `ValidateCandidateDetails`method verifies that the details of a candidate displayed in the application match the expected values provided in the [`OnboardDetails`](./onboard-page.md/#onboarddetails) object. It performs this validation by comparing the displayed values in the UI with the values stored in the [`OnboardDetails`](./onboard-page.md/#onboarddetails) object and logs any discrepancies.

=== "Method Signature"

	```csharp
	public void ValidateCandidateDetails(OnboardDetails onboardDetails, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetails` | [`OnboardDetails`](./onboard-page.md/#onboarddetails) | The expected details of the candidate to validate. |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Retrieve Column Text:
		- Calls GetTextFromColumn for each column header to retrieve the corresponding text value from the table.
	1. Validate and Assert Values:
		- Compares each retrieved value with the expected value from onboardDetails and logs the validation result.
	1. Special Case Handling:
		- Handles specific cases for gender and tax terms, applying different validation rules as necessary.

=== "Usage"

	This method is used to validate the details of a candidate after a successful [`BulkOnboard`](./onboard-page.md/#bulkonboard) operation.
	
	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.ValidateCandidateDetails(onboardDetails, "Validate Candidate Details");
	```

#### ***ManageRole***

---

The `ManageRole` method is designed to search for an employee using their email and first name, then access and manage the employee's role through the application's user interface. It involves searching for the employee, clicking on the "Actions" button associated with them, and then selecting the "Manage Role" option.

=== "Method Signature"

	```csharp
	public void ManageRole(string empMail, string empFirstName, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `empMail` | `string` | The email address of the employee to manage the role for. |
	| `empFirstName` | `string` | The first name of the employee to manage the role for. |
	| `nodeName` | `string` | The name of the node to be shown in the report. |

=== "Functionality"

	1. Search for the employee using their email and first name.
	1. Click on the "Actions" button associated with the employee.
	1. Select the "Manage Role" option from the dropdown menu.

=== "Usage"
	
	This method is used in the [`ManageSupervision`](#managesupervision) method to manage the role of an employee.

	```csharp
	WorkforcePage workforcePage = new WorkforcePage();
	workforcePage.ManageRole("john.doe@example.com", "John", "Manage Employee Role");
	```

#### ***AddCandidateToSupervisor***

---

The `AddCandidateToSupervisor` method adds a candidate to either the supervisor's list of reporting employees or assigned trainees based on the `isTrainee` flag. It handles the UI interactions required to input the candidate's full name, select them from a search result, and verify that the selection has been made.

=== "Method Signature"

	```csharp
	private void AddCandidateToSupervisor(string candidateFullName, bool isTrainee)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `candidateFullName` | `string` | The full name of the candidate to add. |
	| `isTrainee` | `bool` | A flag indicating whether the candidate is a trainee. |

=== "Functionality"

	1. Define Locators:
		- Creates By locators for the search result and selection choice elements.
	1. Determine Input Field:
		- Based on the isTrainee flag, selects the appropriate input field and sends the candidate's full name.
	1. Select Candidate from Search Result:
		- Waits for the search result element to become visible and clicks it.
	1. Verify Selection:
		- Waits for the selection choice element to become visible to confirm that the candidate has been added.

=== "Usage"

	This method is used internally in the [`ManageSupervision`](#managesupervision) method to add candidates to a supervisor's list of reporting employees or assigned trainees.

#### ***AddSupervisorInReportingTo***

---

The `AddSupervisorInReportingTo` method assigns a supervisor to the "Reporting To" field by searching for their full name and selecting them from the search results. It ensures the input field and selection are visible and interactable. This method is used in the [`ManageSupervision`](#managesupervision) method.

=== "Method Signature"

	```csharp
	private void AddSupervisorInReportingTo(string supervisorFullName)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `supervisorFullName` | `string` | The full name of the supervisor to assign. |

=== "Functionality"

	1. Define Locators:
		- Creates By locators for the search result and selection choice elements based on the supervisor's full name.
	1. Click Reporting To Input Field:
		- Waits for the "Reporting To" input field to be visible and clicks it.
	1. Enter Supervisor's Name:
	 	- Waits for the text box within the "Reporting To" field to be visible and sends the supervisor's full name.
	1. Select Supervisor from Search Result:
		- Waits for the search result element to become visible and clicks it to select the supervisor.
	1. Verify Selection:
		- Waits for the selection choice element to become visible to confirm that the supervisor has been successfully added.

=== "Usage"

	This method is used internally in the [`ManageSupervision`](#managesupervision) method to assign a supervisor to the "Reporting To" field.

#### **ClickEllipsisUnderBanner**

---

The `ClickEllipsisUnderBanner` method attempts to click an ellipsis (three-dot menu) element located under a banner. If the click action is intercepted (typically because of a banner overlay), the method will first collapse the banner and then retry clicking the ellipsis.

=== "Method Signature"

	```csharp
	public void ClickEllipsisUnderBanner()
	```
=== "Functionality"

	1. Click Ellipsis:
		- Attempts to click the ellipsis element located under a banner.
	1. Handle Banner Overlay:
		- If the click action is intercepted by a banner overlay, the method will first collapse the banner and then retry clicking the ellipsis.

=== "Usage"

	This method is used to interact with elements located under a banner that may be obscured by the banner itself. It is used in the [`ManageSupervision`](#managesupervision) method.

	```csharp
	WorkforcePage workforcePage = new WorkforcePage(driver);
	workforcePage.ClickEllipsisUnderBanner();
	```

#### **ManageSupervision**

---

The `ManageSupervision` method is used to manage the supervision details for a candidate and their supervisor. It performs actions based on the current URL and the profile details of the candidate and supervisor.

=== "Method Signature"

	```csharp
	public void ManageSupervision(OnboardDetails candidateDetails, OnboardDetails supervisorDetails)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `candidateDetails` | [`OnboardDetails`](./onboard-page.md/#onboarddetails) | The details of the candidate to manage supervision for. |
	| `supervisorDetails` | [`OnboardDetails`](./onboard-page.md/#onboarddetails) | The details of the supervisor to manage supervision for. |

=== "Functionality"

	1. Check Current URL:
		- If the URL contains "/app/profile", it assumes the user is on a profile page.
	1. Manage Supervision on Profile Page:
		- Click the ellipsis menu if visible.
		- Wait for and click the "Manage Role" button.
		- Check if the current profile matches the candidate's name:
			- If yes, add the supervisor to the candidate.
			- If the current profile matches the supervisor's name:
				- Add the candidate as a subordinate to the supervisor.
	1. Manage Supervision in Other Scenarios:
		- If not on the profile page, manage roles directly.
		- Add the candidate to the supervisor's list.
	1. Save Changes:
		- Wait for the "Save" button to be clickable and then click it to save the changes.

=== "Example Usage"

	```csharp
	WorkforcePage workforcePage = new WorkforcePage(driver
	workforcePage.ManageSupervision(candidateDetails, supervisorDetails);
	```
