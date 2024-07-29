# Working with System Files

We will be working with files mainly while using file uploads/downloads or generating reports etc.,

## **File Uploads**

Let's say our current test requires us to upload a file called `sample.pdf` which is present in the `TestData/Files` folder. We can use the following code to upload the file:

=== "UploadFile"
	
	```csharp
	using System.IO;

	public void UploadFile()
	{
		var currentDirectory = Directory.GetCurrentDirectory();
		var filePath = Path.GetFullPath(Path.Combine(currentDirectory, "..", "..", "..", "TestData", "Files", "sample.pdf"));
		// Use the filePath to upload the file
	}
	```
=== "Explanation"

	1. `Directory.GetCurrentDirectory()` - This method returns the current working directory of the application.
	1. `Path.GetFullPath()` - This method returns the absolute path of the file.
	1. `Path.Combine()` - This method combines the specified paths into one path.
	1. `..` - This is used to move up one directory level.

---

## **File Downloads**

Let's say our current test requires us to download a file and we don't exactly know the name of the file being downloaded. So we need to check for the number of the files before and wait for a enw file to be added to the `Downloads` directory. Assuming our `Downloads` directory is in our project directory, below is the code to download the file:

=== "DownloadFile"
	
	```csharp
	using System.IO;

	public void DownloadFile()
	{
		var currentDirectory = Directory.GetCurrentDirectory();
		var downloadsDirectory = Path.GetFullPath(Path.Combine(currentDirectory, "Downloads"));
		var filesCount = Directory.GetFiles(downloadsDirectory).Length;
		// Code to download the file
		// Wait for the file to be downloaded
		while (Directory.GetFiles(downloadsDirectory).Length == filesCount)
		{
			// Wait for the file to be downloaded
		}
	}
	```

=== "Explanation"

	1. `Directory.GetCurrentDirectory()` - This method returns the current working directory of the application.
	1. `Path.GetFullPath()` - This method returns the absolute path of the file.
	1. `Path.Combine()` - This method combines the specified paths into one path.
	1. `Directory.GetFiles()` - This method returns the names of files in the specified directory.
	1. `Length` - This property returns the number of elements in the array.
	1. `while` - This loop will keep running until a new file is added to the `Downloads` directory.
	1. `..` - This is used to move up one directory level.
	1. Important point to note is that using a `while` loop is not recommended in real-time scenarios as it will keep the test running until the file is downloaded. Instead, we can use a `Wait` condition to wait for the file to be downloaded.

---

## **Generating Reports**

While working with Reports we mainly use System Files while creating a report path or storing a screenshot.

### Report Path

Let's say we want to store the report in the `Reports` folder. We can use the following code to generate the report path:

=== "ReportPath"
	
	```csharp
	using System.IO;

	public void ReportPath()
	{
		var currentDirectory = Directory.GetCurrentDirectory();
		var reportsDirectory = Path.GetFullPath(Path.Combine(currentDirectory,"..", "..", "..", "Reports"));
		var reportPath = Path.Combine(reportsDirectory, "report.html");
		// Use the reportPath to store the report
	}
	```
=== "Explanation"

	1. `Directory.GetCurrentDirectory()` - This method returns the current working directory of the application.
	1. `Path.GetFullPath()` - This method returns the absolute path of the file.
	1. `Path.Combine()` - This method combines the specified paths into one path.
	1. `..` - This is used to move up one directory level.

### Screenshot Path

Let's say we want to store the screenshot in the `Screenshots` folder. We can use the following code to generate the screenshot path:

=== "ScreenshotPath"
	
	```csharp
	using System.IO;

	public void ScreenshotPath()
	{
		var currentDirectory = Directory.GetCurrentDirectory();
		var screenshotsDirectory = Path.GetFullPath(Path.Combine(currentDirectory, "..", "..", "..", "Screenshots"));
		var screenshotPath = Path.Combine(screenshotsDirectory, "screenshot.png");
		// Use the screenshotPath to store the screenshot
	}
	```

=== "Explanation"

	1. `Directory.GetCurrentDirectory()` - This method returns the current working directory of the application.
	1. `Path.GetFullPath()` - This method returns the absolute path of the file.
	1. `Path.Combine()` - This method combines the specified paths into one path.
	1. `..` - This is used to move up one directory level.