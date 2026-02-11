# Selenium Java Automation Framework

A comprehensive test automation framework built with Selenium WebDriver, TestNG, and Page Object Model (POM) design pattern.

## Features

- ✅ **Selenium WebDriver 4.15.0** - Latest WebDriver version
- ✅ **TestNG Framework** - Powerful testing framework with flexible test configuration
- ✅ **Page Object Model** - Maintainable and scalable test code structure
- ✅ **WebDriver Manager** - Automatic WebDriver management
- ✅ **Log4j2** - Comprehensive logging support
- ✅ **Base Page & Base Test** - Reusable components for all tests
- ✅ **Multi-browser Support** - Chrome and Firefox support

## Project Structure

```
selenium-automation/
├── src/
│   ├── main/
│   │   └── java/com/automation/
│   │       ├── base/
│   │       │   └── BasePage.java          # Base class for all page objects
│   │       ├── config/
│   │       │   ├── ConfigReader.java      # Configuration management
│   │       │   └── DriverFactory.java     # WebDriver initialization
│   │       └── pages/
│   │           ├── LoginPage.java         # Login page object
│   │           └── HomePage.java          # Home page object
│   └── test/
│       ├── java/com/automation/
│       │   ├── base/
│       │   │   └── BaseTest.java          # Base class for all test classes
│       │   └── tests/
│       │       ├── LoginTests.java        # Login test cases
│       │       └── HomePageTests.java     # Home page test cases
│       └── resources/
│           ├── config.properties          # Configuration properties
│           ├── testng.xml                 # TestNG configuration
│           └── log4j2.xml                 # Logging configuration
├── pom.xml                                # Maven configuration
└── README.md                              # Project documentation
```

## Prerequisites

- **Java 11 or higher**
- **Maven 3.6 or higher**
- **Chrome/Firefox browser**

## Installation

1. Clone the repository:
```bash
git clone https://github.com/pingaleyogesh/yogesh.git
cd yogesh
```

2. Checkout the selenium-automation-project branch:
```bash
git checkout selenium-automation-project
```

3. Install dependencies:
```bash
mvn clean install
```

## Configuration

Update `src/test/resources/config.properties` with your application details:

```properties
app.url=https://your-app.com/login
browser=chrome
implicit.wait=10
explicit.wait=15
```

## Running Tests

### Run all tests:
```bash
mvn clean test
```

### Run specific test class:
```bash
mvn clean test -Dtest=LoginTests
```

### Run specific test method:
```bash
mvn clean test -Dtest=LoginTests#testSuccessfulLogin
```

### Run tests with specific browser:
```bash
mvn clean test -DbrowserName=firefox
```

## Test Cases Included

### Login Tests (`LoginTests.java`)
- ✅ Successful login with valid credentials
- ✅ Login fails with invalid credentials
- ✅ Login with empty username

### Home Page Tests (`HomePageTests.java`)
- ✅ Verify welcome message display
- ✅ Verify user name display
- ✅ Verify logout functionality

## Key Components

### BasePage
Provides common methods for all page objects:
- `click()` - Click elements with wait
- `sendKeys()` - Enter text in elements
- `getText()` - Get text from elements
- `isElementDisplayed()` - Check element visibility
- `navigateTo()` - Navigate to URL

### BaseTest
Provides setup and teardown for all tests:
- `setUp()` - Initialize WebDriver before each test
- `tearDown()` - Close WebDriver after each test

### ConfigReader
Centralized configuration management:
- Read properties from `config.properties`
- Get application URL, browser, wait times

### DriverFactory
WebDriver management:
- Initialize WebDriver based on browser type
- Support for Chrome and Firefox
- ThreadLocal WebDriver management

## Adding New Tests

1. Create a new Page Object in `src/main/java/com/automation/pages/`:

```java
public class DashboardPage extends BasePage {
    @FindBy(id = "dashboard-title")
    private WebElement dashboardTitle;
    
    public DashboardPage(WebDriver driver) {
        super(driver);
    }
    
    public String getDashboardTitle() {
        return getText(dashboardTitle);
    }
}
```

2. Create a new Test Class in `src/test/java/com/automation/tests/`:

```java
public class DashboardTests extends BaseTest {
    @Test(description = "Verify dashboard displays title")
    public void testDashboardTitle() {
        DashboardPage dashboardPage = new DashboardPage(driver);
        Assert.assertTrue(dashboardPage.getDashboardTitle().contains("Dashboard"));
    }
}
```

3. Add test configuration in `testng.xml`

## Best Practices

1. ✅ Use Page Object Model - One page object per page
2. ✅ Explicit waits - Use WebDriverWait for element interactions
3. ✅ Logging - Log all important actions and errors
4. ✅ Configuration management - Use config.properties for environment details
5. ✅ Base classes - Extend BasePage and BaseTest for code reusability
6. ✅ Meaningful test names - Use descriptive test method names
7. ✅ Single responsibility - Each test should test one feature

## Logging

Logs are configured in `log4j2.xml`:
- **Console output** - Real-time test execution logs
- **File output** - `logs/automation.log` - Detailed logs
- **Rolling logs** - Automatic log rotation based on size and date

## Troubleshooting

### Issue: WebDriver not found
**Solution**: WebDriverManager will automatically download the correct driver version

### Issue: Element not found
**Solution**: Check if wait times are sufficient in `config.properties`

### Issue: Tests fail intermittently
**Solution**: Increase explicit wait time in `config.properties`

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is licensed under the MIT License

## Author

[pingaleyogesh](https://github.com/pingaleyogesh)

## Support

For support, please open an issue on GitHub.