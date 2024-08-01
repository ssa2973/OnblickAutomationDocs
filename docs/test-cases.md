# Writing Proper Test Cases

## **Introduction**

---

Writing detailed and effective manual test cases is essential for ensuring the quality and reliability of the application. This guide provides best practices and guidelines for creating comprehensive and maintainable manual test cases.

## **Best Practices**

---

1. **Understand the Requirements**
	- Review Requirements: Ensure a thorough understanding of the functional and non-functional requirements.
	- Identify Test Scenarios: Determine the key scenarios that need to be tested.
1. **Use Clear and Descriptive Titles**
	- Meaningful Titles: Use clear and descriptive titles for your test cases.
	- Consistent Naming Conventions: Follow a consistent naming convention for better readability.
1. **Write Detailed Descriptions**
	- Test Case Description: Provide a detailed description of what the test case is intended to validate.
	- Purpose: Clearly state the purpose of the test case.
1. **Define Pre-Conditions**
	- Setup Conditions: Specify any pre-conditions that must be met before executing the test case.
	- Initial State: Describe the initial state of the system before the test is executed.
1. **Write Step-by-Step Instructions**
	- Detailed Steps: Provide clear and detailed step-by-step instructions for executing the test case.
	- Actions and Inputs: Include specific actions and inputs required at each step.
1. **Specify Expected Results**
	- Expected Outcome: Clearly define the expected result for each step.
	- Pass/Fail Criteria: Provide criteria for determining whether the test case has passed or failed.
1. **Include Test Data**
	- Test Data: Specify any test data required for executing the test case.
	- Data Variations: Include variations of data to cover different scenarios.
1. **Use Attachments and References**
	- Screenshots: Include screenshots or mockups to illustrate the steps and expected results.
	- References: Provide references to related documents or specifications.
1. **Review and Update Regularly**
	- Peer Reviews: Conduct regular reviews to ensure test case quality.
	- Keep Updated: Update test cases regularly to reflect any changes in requirements or functionality.

## **Example Test Case**

---

Here is an example of a well-written manual test case:

### Test Case Title: Verify Successful User Login

#### Description

Verifies that a user can successfully log in with valid credentials.

#### Pre-Conditions

- User is on the login page.
- User has a valid username and password.

#### Test Steps

1. **Navigate to Login Page**
	- Action: Open the login page URL in the browser.
	- Expected Result: Login page is displayed.
1. **Enter Username**
	- Action: Enter the valid username in the username field.
	- Expected Result: Username is entered correctly.
1. **Enter Password**
	- Action: Enter the valid password in the password field.
	- Expected Result: Password is entered correctly.
1. **Click Login Button**
	- Action: Click the "Login" button.
	- Expected Result: User is redirected to the dashboard page.
1. **Verify Dashboard Page**
	- Action: Check if the dashboard page is displayed.
	- Expected Result: Dashboard page is displayed with the correct user information.

#### Expected Results

- User should be successfully logged in and redirected to the dashboard page.

#### Test Data

- Username: `testuser`
- Password: `password123`

#### Attachments
- Screenshot of the login page
- Screenshot of the dashboard page after successful login