# Project Structure

The project structure is subject to change, refer to the [latest source](https://onblickrigaps.visualstudio.com/Automation/_git/Selenium2.0){:target="_blank"} for more up-to-date structure. It is organized to separate test logic from page object definitions. Below is a generalized representation of project structure:

=== "Folder Structure"
```bash
.
├── README.md
└── HR Modules
	├── Common_Modules
	├── Downloads
	├── Environment_URLs
	│	├── endpoints-config.json
	│	├── env-config.json
	│	├── Environment.cs
	│	└──	URLs.cs
	├── PageObjects
	│	├── LoginPage.cs
	│	├── OnboardPage.cs
	│	├── SettingsPage.cs
	│	├── TimesheetPage.cs
	│	├── <Module>
	│	│	├── <PageName>Page.cs
	│	│	└──	etc.,
	│	└──	etc.,
	├── Reports
	│	├── Report <dd_MMM_yyy>
	│	│	├── Screenshots
	│	│	│	├── Screenshot_<H_mm_ss>.png
	│	│	│	└──	etc.,
	│	│	├── ExtentReport - <dd_MMM_yy - hh_mm>.html
	│	│	└──	etc.,
	│	└──	etc.,
	├── TestData
	│	│── Files
	│	│	├── SampleDoc.pdf
	│	│	├── Section3SampleDoc.jpg
	│	│	└──	etc.,
	│	│── LoginCredentials
	│	│	├── creds.json
	│	│	└── LoginCreds.cs
	│	│── RandomNameGenerator
	│	│	├── names.json
	│	│	└── RandomEmployeeDetailsGenerator.cs
	│	├── <TestName>_TestData.cs
	│	└──	etc.,
	├── TestPlans
	│	├── <TestModule>
	│	│	├── <TestName>.cs
	│	│	└──	etc.,
	│	└──	etc.,
	├── Utilities
	│	├── RandomLcaGenerator
	│	│	├── LcaPdfFormMapper.cs
	│	│	├── LcaPdfFormStructure.cs
	│	│	└── RandomLcaDetailsGenerator.cs
	│	├── AttributeExtensions.cs
	│	├── BrowserOptions.cs
	│	├── ExcelHelper.cs
	│	├── ExcludeLeaveCalculation.cs
	│	├── PdfHelper.cs
	│	├── ReportsGenerationClass.cs
	│	├── SoftAssertion.cs
	│	├── TestExecutionHelper.cs
	│	├── WaitHelpers.cs
	│	└──	WebElementExtensions.cs
	├── WebInteractions
	│	├── I983Interactions.cs
	│	├── I9Interactions.cs
	│	├── LCAInteractions.cs
	│	├── ProjectInteractions.cs
	│	├── SignRequestInteractions.cs
	│	└──	TimesheetInteractions.cs
	│──	HR Modules.csproj
	└──	HR Modules.sln


```

