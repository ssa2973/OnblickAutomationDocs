# OnboardPage

The `OnboardPage` contains all the classes, locators and methods necessary to interact with the Onboard page.

## Members

### **Classes**

The `OnboardPage` class contains the following classes:

#### **OnboardDetails**

---

The `OnboardDetails` class is designed to hold and manage employee onboarding information. It encapsulates various personal and employment-related details for an employee.

=== "Constructor"

	```csharp
	public OnboardDetails(
        string taxTerms,
        string firstName,
        string lastName,
        string designation,
        string email,
        string phone,
        string employmentType,
        string employeeID = null,
        string dob = null,
        string gender = null,
        string address1 = null,
        string address2 = null,
        string city = null,
        string state = null,
        string zip = null,
        string startDate = null,
        string workAuthType = null,
        bool? isBilling = null,
        string wageRate = null,
        string wageFrom = null,
        string wageTo = null,
        string wageCycle = null,
        string department = null,
        string reportingTo = null,
        bool? isTrainee = null
    )
	```

=== "Parameters"

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | `taxTerms` | `string` | The tax terms under which the employee is employed. |
    | `firstName` | `string` | The first name of the employee. |
    | `lastName` | `string` | The last name of the employee. |
    | `designation` | `string` | The job title or designation of the employee. |
    | `email` | `string` | The email address of the employee. |
    | `phone` | `string` | The phone number of the employee. |
    | `employmentType` | `string` | The type of employment (e.g., full-time, part-time). |
    | `employeeID` | `string` | The unique identifier for the employee. Default is `null`. |
    | `dob` | ``string`` | The date of birth of the employee. Default is ``null``. |
    | `gender` (optional) | `string` | The gender of the employee. Default is ``null``. |
    | `address1` (optional) | `string` | The primary address line of the employee. Default is ``null``. |
    | `address2` (optional) | `string` | The secondary address line of the employee. Default is `null`. |
    | `city` (optional) | `string` | The city of the employee's address. Default is `null`. |
    | `state` (optional) | `string` | The state of the employee's address. Default is `null`. |
    | `zip` (optional) | `string` | The ZIP code of the employee's address. Default is `null`. |
    | `startDate` (optional) | `string` | The start date of employment or contract. Default is `null`. |
    | `workAuthType` (optional) | `string` | The type of work authorization the employee has. Default is `null`. |
    | `isBilling` (optional) | `bool?` | Indicates if the employee is billable. Default is `null`. |
    | `wageRate` (optional) | `string` | The wage rate of the employee. Default is `null`. |
    | `wageFrom` (optional) | `string` | The minimum wage rate of the employee. Default is `null`. |
    | `wageTo` (optional) | `string` | The maximum wage rate of the employee. Default is `null`. |
    | `wageCycle` (optional) | `string` | The wage cycle (e.g., weekly, bi-weekly). Default is `null`. |
    | `department` (optional) | `string` | The department to which the employee belongs. Default is `null`. |
    | `reportingTo` (optional) | `string` | The supervisor or manager the employee reports to. Default is `null`. |
    | `isTrainee` (optional) | `bool?` | Indicates if the employee is a trainee. Default is `null`. |

=== "Properties"

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | `FirstName` | `string` | The first name of the employee. |
    | `LastName` | `string` | The last name of the employee. |
    | `Designation` | `string` | The job title or designation of the employee. |
    | `EmployeeID` | `string` | The unique identifier for the employee. |
    | `Email` | `string` | The email address of the employee. |
    | `Phone` | `string` | The phone number of the employee. |
    | `Dob` | `string` | The date of birth of the employee. |
    | `Gender` | `string` | The gender of the employee. |
    | `Address1` | `string` | The primary address line of the employee. |
    | `Address2` | `string` | The secondary address line of the employee. |
    | `City` | `string` | The city of the employee's address. |
    | `State` | `string` | The state of the employee's address. |
    | `Zip` | `string` | The ZIP code of the employee's address. |
    | `EmploymentType` | `string` | The type of employment (e.g., full-time, part-time). |
    | `TaxTerms` | `string` | The tax terms under which the employee is employed (e.g., W2, C2C, 1099). |
    | `EmploymentStartDate` | `string` | The start date of employment for W2 employees. |
    | `ContractStartDate` | `string` | The start date of contract for C2C or 1099 employees. |
    | `WorkAuthType` | `string` | The type of work authorization the employee has. |
    | `IsBilling` | `bool` | Indicates if the employee is billable. |
    | `WageRate` | `string` | The wage rate of the employee. |
    | `WageFrom` | `string` | The minimum wage rate of the employee. |
    | `WageTo` | `string` | The maximum wage rate of the employee. |
    | `WageCycle` | `string` | The wage cycle (e.g., weekly, bi-weekly). |
    | `Department` | `string` | The department to which the employee belongs. |
    | `ReportingTo` | `string` | The supervisor or manager the employee reports to. |
    | `IsTrainee` | `bool` | Indicates if the employee is a trainee. |
    | `IsTraineeText` | `string` | A textual representation of whether the employee is a trainee ("y" for yes, "n" for no). |

=== "Constructor Logic"

    - Initializes properties with provided values.
    - Sets `EmploymentStartDate` or `ContractStartDate` based on `TaxTerms`.
    - Determines `IsTrainee` based on `TaxTerms` and `WorkAuthType`.
    - Sets `IsTraineeText` based on `IsTrainee` and `TaxTerms`.

=== "Example Usage"

    ```csharp
    var onboardDetails = new OnboardDetails(
        taxTerms: "W2",
        firstName: "John",
        lastName: "Doe",
        designation: "Software Engineer",
        email: "john.doe@example.com",
        phone: "123-456-7890",
        employmentType: "Full-Time",
        startDate: "2023-01-01",
        workAuthType: "US Citizen"
    );
    ```

#### OnboardDetailsMap

---

The `OnboardDetailsMap` class is a mapping configuration for the `OnboardDetails` class. It is used to map CSV columns to the properties of the `OnboardDetails` class using the `CsvHelper` library.

=== "Constructor"
    
    ```csharp
    public class OnboardDetailsMap : ClassMap<OnboardDetails>
    {
        public OnboardDetailsMap()
        {
            Map(m => m.FirstName).Name("First Name*");
            Map(m => m.LastName).Name("Last Name*");
            Map(m => m.Designation).Name("Designation*");
            Map(m => m.EmployeeID).Name("Employee ID");
            Map(m => m.Dob).Name("Date of Birth").TypeConverterOption.Format("M/d/yyyy");
            Map(m => m.Gender).Name("Gender");
            Map(m => m.Phone).Name("Phone Number*");
            Map(m => m.Email).Name("Email ID*");
            Map(m => m.EmploymentType).Name("Employment Type*");
            Map(m => m.EmploymentStartDate).Name("Employment Start Date+").TypeConverterOption.Format("M/d/yyyy");
            Map(m => m.ContractStartDate).Name("Contract Start Date+").TypeConverterOption.Format("M/d/yyyy");
            Map(m => m.Address1).Name("Address Line 1");
            Map(m => m.Address2).Name("Address Line 2");
            Map(m => m.City).Name("City");
            Map(m => m.State).Name("State");
            Map(m => m.Zip).Name("Zip Code");
            Map(m => m.TaxTerms).Name("Tax Terms*");
            Map(m => m.WorkAuthType).Name("Work Authorization Type+");
            Map(m => m.WageRate).Name("Wage Rate (Offered Salary)");
            Map(m => m.WageCycle).Name("Wage Cycle");
            Map(m => m.Department).Name("Department");
            Map(m => m.ReportingTo).Name("Reporting To Email");
            Map(m => m.IsTraineeText).Name("IsTrainee");
        }
    }
    ```

=== "Mapped Properties"

	| CSV Column | Property |
	| ---------- | -------- |
	| First Name* | `FirstName` |
	| Last Name* | `LastName` |
	| Designation* | `Designation` |
	| Employee ID | `EmployeeID` |
	| Date of Birth | `Dob` |
	| Gender | `Gender` |
	| Phone Number* | `Phone` |
	| Email ID* | `Email` |
	| Employment Type* | `EmploymentType` |
	| Employment Start Date+ | `EmploymentStartDate` |
	| Contract Start Date+ | `ContractStartDate` |
	| Address Line 1 | `Address1` |
	| Address Line 2 | `Address2` |
	| City | `City` |
	| State | `State` |
	| Zip Code | `Zip` |
	| Tax Terms* | `TaxTerms` |
	| Work Authorization Type+ | `WorkAuthType` |
	| Wage Rate (Offered Salary) | `WageRate` |
	| Wage Cycle | `WageCycle` |
	| Department | `Department` |
	| Reporting To Email | `ReportingTo` |
	| IsTrainee | `IsTraineeText` |

=== "Example Usage"

	```csharp
	using CsvHelper;
    using CsvHelper.Configuration;
    using System.Globalization;
    using System.IO;

    public class Program
    {
        public static void Main()
        {
            using (var reader = new StreamReader("path/to/your/csvfile.csv"))
            using (var csv = new CsvReader(reader, new CsvConfiguration(CultureInfo.InvariantCulture)
            {
                Delimiter = ",",
                HasHeaderRecord = true,
            }))
            {
                csv.Context.RegisterClassMap<OnboardDetailsMap>();
                var records = csv.GetRecords<OnboardDetails>().ToList();
            
                foreach (var record in records)
                {
                    Console.WriteLine($"First Name: {record.FirstName}, Last Name: {record.LastName}");
                }
            }
        }
    }
	```
    _Note: This is only an example implementation on how to use it. This `ClassMap` is already used in [`BulkOnboard`](#bulkonboard) functionality_.

### **Locators**

---

The locators used in the `OnboardPage` class aren't disclosed here, you can go through the `OnboardPage.cs` file in the project to view the locators. All locator members are of two types `By` and `IWebElement`(using `PageObjectFactory`).

### **Methods**

---

There are several methods in the `OnboardPage` class that are used to interact with the Onboard page. Some of the methods are private and some are public, italicized methods are private methods.

#### **SingleOnboard**

---

The `SingleOnboard` method is designed to onboard a single employee using the details provided in an [`OnboardDetails`](#onboarddetails) type object.

=== "Method Signature"

	```csharp
	public void SingleOnboard(OnboardDetails onboardDetails, string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetails` | `OnboardDetails` | The employee details to onboard. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Functionality"

    - **Initialization**: Sets `nodeName` to "Onboard" if it is null. Extracts individual properties from the `onboardDetails` object.
    - **Navigation**: Navigates to the single onboard URL.
    - **Input **Fields: Fills in the input fields with the provided employee details.
    - **Logging**: Logs each substep to the report to provide detailed feedback on the progress of the onboarding process.
    - **Submission**: Clicks the onboard button to submit the form.

=== "Example Usage"

    ```csharp
    var onboardDetails = new OnboardDetails(
        taxTerms: "W2",
        firstName: "Jane",
        lastName: "Doe",
        designation: "Software Engineer",
        email: "jane.doe@example.com",
        phone: "123-456-7890",
        employmentType: "Full-Time",
        startDate: "2023-01-01",
        workAuthType: "Citizen"
    );

    SingleOnboard(onboardDetails);

    ```

#### ***DownloadMultiOnboardCsv***

--- 

The `DownloadMultiOnboardCsv` method navigates to the bulk onboarding URL, downloads a CSV file for multiple onboardings, and returns the path of the downloaded file.

=== "Method Signature"

	```csharp
	public string DownloadMultiOnboardCsv(string nodeName = null)
	```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Functionality"
    
    - **Navigation**: Navigates to the bulk onboard URL.
    - **Initialization**: Determines the download path and initial file count in the directory.
    - **Download CSV**: Clicks the download button for the bulk onboarding CSV.
    - **Wait for Download**: Waits for the download to complete and retrieves the latest downloaded file.
    - **File Validation**: Ensures the downloaded file is not a temporary or incomplete file.
    - **Return File Path**: Returns the full path of the downloaded file.

=== "Example Usage"
    
    ```csharp
    string downloadedCsvPath = DownloadMultiOnboardCsv("BulkOnboard");
    Console.WriteLine($"Downloaded CSV path: {downloadedCsvPath}");
    ```

#### ***WriteOnboardDetailsToCsv***

---

The `WriteOnboardDetailsToCsv` method writes a list of `OnboardDetails` objects to a CSV file. The method can either create a new CSV file or overwrite an existing one.

=== "Method Signature"
    
    ```csharp
    private string WriteOnboardDetailsToCsv(string filePath, List<OnboardDetails> onboardDetailsList, string nodeName = null)
    ```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `filePath` | `string` | The path of the CSV file to write the onboard details to. |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to write to the CSV file. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Functionality"

    1. **Open/Create CSV File**:
        - Opens the file at filePath for reading and writing, allowing shared access for reading and writing.
        - Uses a StreamWriter to write to the file.
        - Uses CsvWriter from the CsvHelper library to handle CSV writing with the specified culture (CultureInfo.InvariantCulture).
    1. **Register Class Map and Write Header**:
        - Registers the OnboardDetailsMap class map to define the CSV column mappings.
        - Writes the header row for the OnboardDetails class.
        - Moves to the next record to begin writing data rows.
    1. **Write Onboard Details**:
        - Writes each OnboardDetails object in onboardDetailsList to the CSV file.
    1. **Exception Handling**:
        - Catches any exceptions that may occur and handles them appropriately (e.g., logging the exception).
    1. Return File Path:
        - Returns the path of the CSV file after writing is complete.

=== "Example Usage"

    ```csharp
    List<OnboardDetails> onboardDetailsList = new List<OnboardDetails>
    {
        new OnboardDetails("W2", "John", "Doe", "Developer", "john.doe@example.com", "1234567890", "Full-Time"),
        new OnboardDetails("C2C", "Jane", "Smith", "Manager", "jane.smith@example.com", "0987654321", "Contractor")
    };

    string filePath = "path/to/onboard_details.csv";
    string resultFilePath = WriteOnboardDetailsToCsv(filePath, onboardDetailsList, "OnboardDetailsWrite");
    Console.WriteLine($"CSV file written to: {resultFilePath}");
    ```

#### ***ValidateImportedData***

---

The `ValidateImportedData` method validates the details of onboarded candidates from a provided list against the data displayed on a web page. It performs the validation by comparing the data in the `OnboardDetails` objects to the corresponding elements on the web page.

=== "Method Signature"

    ```csharp
    private void ValidateImportedData(List<OnboardDetails> onboardDetailsList, string nodeName = null)
    ```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Functionality"

    1. Define Index Mappings:
        - Defines the index positions for various fields in the table on the web page.
    1. Dynamic Locators:
        - Defines `dynamicLocatorFixed` and `dynamicLocator` methods to generate XPath locators for table cells.
    1. Validation Loop:
        - Iterates through each `OnboardDetails` object in the list.
        - Generates the XPath locators for the corresponding fields.
        - Validates each field (e.g., `FirstName`, `LastName`, `Designation`, etc.) by comparing the text in the web element to the value in the `OnboardDetails` object.
        - Scrolls to and highlights the element before validation for visual verification.
        - Unhighlights the element after validation.
    1. Special Handling:
        - For `Gender`, checks if the value is "I choose not to disclose" and validates accordingly.
        - For `EmploymentStartDate` vs. `ContractStartDate`, chooses the correct field based on the `TaxTerms`.
        - For `IsTrainee`, sets the expected value based on conditions and validates it.

=== "Example Usage"

    ```csharp
    List<OnboardDetails> onboardDetailsList = new List<OnboardDetails>
    {
        new OnboardDetails("W2", "John", "Doe", "Developer", "john.doe@example.com", "1234567890", "Full-Time"),
        new OnboardDetails("C2C", "Jane", "Smith", "Manager", "jane.smith@example.com", "0987654321", "Contractor")
    };

    ValidateImportedData(onboardDetailsList, "OnboardDetailsValidation");
    ```

#### ***SkipImport***

--- 

The `SkipImport` method processes a list of onboarded candidate details, identifies any failed or duplicate records, and skips their import. This method interacts with web elements to resolve conflicts and update the list of onboard details accordingly.

=== "Method Signature"

    ```csharp
    private List<OnboardDetails> SkipImport(List<OnboardDetails> onboardDetailsList, string nodeName = null)
    ```
=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Returns"

	- A list of `OnboardDetails` objects that are ready for import after resolving any conflicts.

=== "Functionality"

    1. Define Element Locators:
        - `emailColumnLocator`: Locator for the email column in the table.
        - `UploadCsvResolveNowBtn`, `SkipImportBtnId()`, `SkipImportProceedBtnId()`: Locators for buttons involved in the process.
    1. Initialize List:
        - `failedOrDuplicateDetailsList`: List to store details of failed or duplicate records.
    1. Wait and Click:
        - Waits for the `UploadCsvResolveNowBtn` to become clickable. If it times out, the method skips to the end.
        - Clicks the resolve button (`resolveNowBtn`).
        - Waits for the invisibility of the `OnblickLogoId` element to ensure the page has updated.
    1. Email Comparison:
        - Finds all elements in the email column.
        - Iterates through the emails and compares each with the emails in the `onboardDetailsList`.
        - Adds matching records to the `failedOrDuplicateDetailsList`.
    1. Update List:
        - Removes the failed or duplicate records from the `onboardDetailsList`.
    1. Additional Clicking and Logging:
        - Waits for the skip import button to become clickable, clicks it, and then clicks the proceed button.
        - Logs the substep indicating the import was skipped for failed/duplicate records.
        - Waits for the invisibility of the `OnblickLogoId` element.

=== "Example Usage"

    This method is used in the [`TrySkipAndValidate`](#tryskipandvalidate) method.

    ```csharp
    List<OnboardDetails> onboardDetailsList = /* list of onboard details*/;
    onboardDetailsList = SkipImport(onboardDetailsList, "SkipImportNode");
    ```

#### ***TrySkipAndValidate***

---

The `TrySkipAndValidate` method processes a list of `OnboardDetails` by first skipping the import of failed or duplicate records and then validating the imported data. This ensures that the onboarded data is accurate and free of conflicts. Uses both [`SkipImport`](#skipimport) and [`ValidateImportedData`](#validateimporteddata) methods.

=== "Method Signature"

    ```csharp
    private List<OnboardDetails> TrySkipAndValidate(List<OnboardDetails> onboardDetailsList, string nodeName = null)
    ```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Returns"

	- A list of `OnboardDetails` objects that have been successfully imported and validated.

=== "Functionality"

	1. **Skip Import**:
		- Calls the [`SkipImport`](#skipimport) method to skip the import of failed or duplicate records.
	1. **Validate Imported Data**:
		- Calls the [`ValidateImportedData`](#validateimporteddata) method to validate the imported data.
	1. **Return List**:
		- Returns the updated list of onboard details after skipping and validation.

#### ***UploadCsv***

---

The `UploadCsv` method is responsible for uploading a CSV file containing onboarding details to the web application, navigating through the upload process, and ensuring the completion of the upload.

=== "Method Signature"

	```csharp
	private void UploadCsv(string filePath, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `filePath` | `string` | The path of the CSV file to upload. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Functionality"

    1. Navigate to Bulk Onboard URL:
        - Checks if the current URL is the bulk onboarding URL. If not, it navigates to the correct URL.
    1. Upload CSV File:
        - Waits for the CSV upload element to exist.
        - Uploads the CSV file using the SendKeys method.
    1. Navigate Through Upload Process:
        - Waits for the "Next" button to be clickable and clicks it.
        - Waits for the OnBlick logo to become invisible.
        - Checks if the onboard candidates label is displayed and refreshes the page until it's not visible.
    1. Handle Upload Completion:
        - Waits for the "Go to Uploads" button to be clickable and clicks it.

=== "Example Usage"

    ```csharp
    string csvFilePath = @"C:\path\to\your\csvfile.csv";
    UploadCsv(csvFilePath, "Upload Csv");
    ```

#### ***CancelImport***

---

The `CancelImport` method cancels the import process of a CSV file containing onboarding details. It interacts with web elements to cancel the import process and ensures the process is successfully canceled.

=== "Method Signature"

	```csharp
	private void CancelImport()
	```

=== "Functionality"

    1. Ensures the "Cancel" button for the CSV upload is clickable.
    1. Clicks the "Cancel" button to initiate the cancellation process.
    1. Ensures the confirmation buttons are clickable.
    1. Clicks the "No" button to dismiss the first confirmation dialog.
    1. Clicks the "Cancel" button again to retry the cancellation.
    1. Clicks the "Yes" button to confirm the cancellation.
    1. Waits for the OnBlick logo to become invisible, indicating that the cancellation is complete.


#### ***OnboardCandidates***

---

The `OnboardCandidates` method is used to onboard a selected set of candidates in the web application. It performs actions to select all candidate records and initiate the onboarding process, and then waits for a success popup to appear.

=== "Method Signature"

	```csharp
	private void OnboardCandidates()
	```

=== "Functionality"

	1. Select All Candidates:
		- Waits for the "Select All" checkbox to be clickable and clicks it.
	1. Initiate Onboarding:
		- Waits for the "Onboard" button to be clickable and clicks it.
	1. Wait for Success Popup:
		- Waits for the success popup to appear, indicating that the onboarding process has been initiated.


#### ***EditImportedData***

---

The `EditImportedData` method is used to edit the details of an imported candidate in the web application. It selects a candidate, clicks on edit, updates the details, and saves the changes.

=== "Method Signature"

    ```csharp
    private List<OnboardDetails> EditImportedData(List<OnboardDetails> onboardDetailsList, string nodeName = null)
    ```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Returns"

	- A list of `OnboardDetails` objects that have been successfully edited.

=== "Functionality"

    1. Initialize Variables:
        - Define locators for modal buttons, fields, and record colors.
        - Create a list to hold records with duplicate issues and initialize an updated list of onboard details.
    1. Identify and Delete Duplicate Records:
        - Find records with a specific background color indicating duplication.
        - For each duplicate record:
            - Locate the delete button and the email address.
            - Delete the record by clicking the "Delete" button and confirm the action.
            - Remove the deleted record from the list and log the action.
    1. Edit or Delete Records:
        - For each record in the onboard details list:
        - Randomly decide whether to edit or delete the record.
        - Perform actions based on the decision:
            - Edit:
                - Open the edit modal, perform necessary changes, and save the changes.
                - If the record's gender is "I choose not to disclose", handle it with a specific select element.
                - Handle missing mandatory fields by selecting options or typing in values.
            - Delete:
                - Open the delete modal, click "No" to cancel, and then click "Delete" to confirm.
                - Remove the deleted record from the list and log the action.
    1. Return Updated List:
        - Return the updated list of onboard details.

=== "Usage"

    This method is used in the [`ResolveErrors`](#resolveerrors) method.
    
	```csharp
    List<OnboardDetails> onboardDetailsList = /* list of onboard details*/;
	onboardDetailsList = EditImportedData(onboardDetailsList, "EditImportedDataNode");
	```

#### ***ResolveErrors***

---

The ResolveErrors method aims to handle errors in the onboarding process by clicking the "Resolve Now" button and then editing the imported data using [`EditImportedData`](#editimporteddata) to resolve any issues. This method returns the updated list of onboard details after making necessary adjustments.

=== "Method Signature"

	```csharp
    private List<OnboardDetails> ResolveErrors(List<OnboardDetails> onboardDetailsList, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Returns"

	- A list of `OnboardDetails` objects that have been successfully resolved.

=== "Functionality"

	1. **Handle Resolve Now Button**:
		- Waits for the "Resolve Now" button to be clickable and clicks it.
		- Waits for the OnBlick logo to become invisible, indicating the page has updated.
	1. **Edit Imported Data**:
		- Calls the [`EditImportedData`](#editimporteddata) method to edit the imported data.
	1. **Return Updated List**:
		- Returns the updated list of onboard details after resolving errors.


=== "Usage"

    This method is used in the [`BulkOnboardNegative`](#bulkonboardnegative) method.

    ```csharp
    List<OnboardDetails> onboardDetailsList = /* list of onboard details*/;
    onboardDetailsList = ResolveErrors(onboardDetailsList, "ResolveErrorsNode");
    ```

#### **BulkOnboard**

--- 

The `BulkOnboard` method is used to perform bulk onboarding of candidates by uploading a CSV file containing their details. It interacts with web elements to upload the CSV file, resolve any conflicts, and validate the imported data. Tihs method uses the [`DownloadMultiOnboardCsv`](#downloadmultionboardcsv), [`WriteOnboardDetailsToCsv`](#writeonboarddetailstocsv), [`UploadCsv`](#uploadcsv), [`TrySkipAndValidate`](#tryskipandvalidate), [`OnboardCandidates`](#onboardcandidates) methods.

=== "Method Signature"

	```csharp
    public List<OnboardDetails> BulkOnboard(List<OnboardDetails> onboardDetailsList, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Returns"

	- A list of `OnboardDetails` objects that have been successfully onboarded.

=== "Functionality"

	1. **Download CSV**:
		- Calls the [`DownloadMultiOnboardCsv`](#downloadmultionboardcsv) method to download the CSV file.
	1. **Write to CSV**:
		- Calls the [`WriteOnboardDetailsToCsv`](#writeonboarddetailstocsv) method to write the onboard details to the CSV file.
	1. **Upload CSV**:
		- Calls the [`UploadCsv`](#uploadcsv) method to upload the CSV file.
	1. **Try Skip and Validate**:
		- Calls the [`TrySkipAndValidate`](#tryskipandvalidate) method to skip and validate the imported data.
    1. **Onboard Candidates**:
        - Calls the [`OnboardCandidates`](#onboardcandidates) method to onboard the candidates.
	1. **Return Updated List**:
		- Returns the updated list of onboard details after bulk onboarding.

=== "Example Usage"

	```csharp
	List<OnboardDetails> onboardDetailsList = /* list of onboard details*/;
	onboardDetailsList = BulkOnboard(onboardDetailsList, "BulkOnboardNode");
	```

#### **BulkOnboardNegative**

---

The `BulkOnboardNegative` method handles the process of bulk onboarding candidates with an intentional error handling workflow. This includes uploading a CSV file, cancelling the import, resolving any errors, validating the imported data, and onboarding the candidates. The method returns a list of onboard details after successful processing. This method uses the [`DownloadMultiOnboardCsv`](#downloadmultionboardcsv), [`WriteOnboardDetailsToCsv`](#writeonboarddetailstocsv), [`UploadCsv`](#uploadcsv), [`CancelImport`](#cancelimport), [`ResolveErrors`](#resolveerrors), and [`ValidateImportedData`](#validateimporteddata), [`OnboardCandidates`](#onboardcandidates) methods.

=== "Method Signature"

	```csharp
    public List<OnboardDetails> BulkOnboardNegative(List<OnboardDetails> onboardDetailsListIncomplete, List<OnboardDetails> onboardDetailsList, string nodeName = null)
	```

=== "Parameters"

	| Name | Type | Description |
	| ---- | ---- | ----------- |
	| `onboardDetailsListIncomplete` | `List<OnboardDetails>` | The list of incomplete employee details to validate. |
	| `onboardDetailsList` | `List<OnboardDetails>` | The list of complete employee details to validate. |
	| `nodeName` (optional) | `string` | The name of the node to be shown in the report. Default is `null`. |

=== "Returns"

	- A list of `OnboardDetails` objects that have been successfully onboarded."

=== "Functionality"

	1. **Download CSV**:
		- Calls the [`DownloadMultiOnboardCsv`](#downloadmultionboardcsv) method to download the CSV file.
	1. **Write to CSV**:
		- Calls the [`WriteOnboardDetailsToCsv`](#writeonboarddetailstocsv) method to write the onboard details to the CSV file.
	1. **Upload CSV**:
		- Calls the [`UploadCsv`](#uploadcsv) method to upload the CSV file.
	1. **Cancel Import**:
		- Calls the [`CancelImport`](#cancelimport) method to cancel the import process.
	1. **Resolve Errors**:
		- Calls the [`ResolveErrors`](#resolveerrors) method to resolve any errors in the import process.
	1. **Validate Imported Data**:
		- Calls the [`ValidateImportedData`](#validateimporteddata) method to validate the imported data.
	1. **Onboard Candidates**:
		- Calls the [`OnboardCandidates`](#onboardcandidates) method to onboard the candidates.
	1. **Return Updated List**:
		- Returns the updated list of onboard details after bulk onboarding.

=== "Example Usage"

	```csharp
	List<OnboardDetails> onboardDetailsListIncomplete = /* list of incomplete onboard details*/;
	List<OnboardDetails> onboardDetailsList = /* list of onboard details*/;
	List<OnboardDetails> onboardedDetails = BulkOnboardNegative(onboardDetailsListIncomplete, onboardDetailsList, "BulkOnboardNegativeNode");
	```
