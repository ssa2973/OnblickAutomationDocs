# BrowserOptions

## **DefaultChromeOptions**

---

The `DefaultChromeOptions` class extends `ChromeOptions` to provide a default configuration for Chrome WebDriver instances.

### Configuration Details
1. **Download Directory**:
	- Path: `..\..\..\Downloads` (relative to the current execution directory).
	- Ensures the directory is created if it does not exist.
1. **Logging Preferences**:
	- Browser logs: Set to `LogLevel.Severe`.
	- Performance logs: Set to `LogLevel.All`.
1. **Chrome Arguments**:
	- `--disable-extensions`: Disables any extensions.
	- `--disable-popup-blocking`: Disables popup blocking.
	- `--start-maximized`: Maximizes the browser window.
	- `--foreground-flash-enabled`: Brings the window to the foreground.
	- `--window-size=1920x1080`: Sets the screen resolution to 1920x1080 for functional tests.
	- `--headless`: (Commented out) Executes tests in headless mode.

_Note: Only Chrome Browser is used for automation as of now. More browsers shall be used in the future for cross-browser testing._