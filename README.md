# Publix Mobile App Automation Repository

Java Appium Test Framework for Android. This is a Test Automation project that uses Nodejs, Appium 2.0,
Amazon Corretto Java 11, TestNG, Cucumber and Extent Reports for macOS. This framework utilizes the Page Object Model to store an
object repository of reusable mobile elements and reusable driver actions with the help of commonly used utility
methods.

## Prerequisites 

### Manual Setup (Recommended)

1. [Node.js](https://nodejs.org/en/) LTS should be installed on the machine via "nvm" or "homebrew" (Recommended)
   1. [Homebrew](https://brew.sh/) **(Recommended)**
      1. Install homebrew 
         ```bash
         /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
         ```
      2. Open a terminal and type `brew update`. This updates homebrew with a list of the latest versions of node.
      3. Type `brew install node`
   2. [nvm](https://github.com/nvm-sh/nvm). (Only if homebrew cannot be used)
      1. Using their "Install & Update" curl script in the
         terminal. 
         ```bash
         curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
         ```
      2. After installation, create a .zshrc file in your home directory `touch ~/.zshrc`. Copy/paste the following to the
         .zshrc file:
         ```bash
         export NVM_DIR="$HOME/.nvm"
         [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
         [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
         ```
      3. Now source your .zshrc file in terminal `source ~/.zshrc`.

      4. In the terminal install nodejs with the following:
         `nvm install --lts`

      5. Verify node is installed in the terminal with `node --version`

2. Android Studio should be installed via the Publix Self Service app 
   - Alternatively, it can be found [here](https://developer.android.com/studio) and should be installed in the default installation directory
3. `ANDROID_HOME` environment variable should point to the android studio sdk along with appropriate tools added to path
   in `.zshrc` . Copy/Paste the following lines to the `~/.zshrc` file, create it if it not exists.
   ```bash
    export ANDROID_HOME=/Users/$(whoami)/Library/Android/sdk
    export PATH=$PATH:$ANDROID_HOME/platform-tools
    export PATH=$PATH:$ANDROID_HOME/tools
    export PATH=$PATH:$ANDROID_HOME/tools/bin
    export PATH=$PATH:$ANDROID_HOME/emulator
    ```

4. Install [Amazon Corretto Java 11](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html) for
   macOS x64. Then copy/paste the JAVA_HOME environment variable to your `.zshrc` file.

   ```bash
   export JAVA_HOME=/Library/Java/JavaVirtualMachines/amazon-corretto-11.jdk/Contents/Home
   ```

   In your terminal reload the changes by entering:
   ```source ~/.zshrc```.

5. [Appium 2.0](https://appium.github.io/appium/docs/en/2.0/) should be installed via nodejs globally by entering in
   terminal
   ```bash
   npm install -g appium@next`.
   ``` 
   To verify appium is installed correctly with all necessary dependencies
   use [appium-doctor](https://github.com/appium/appium-doctor)
   ```bash
   npm install -g appium-doctor
   ```

6. Install the iOS and Android appium drivers by running the terminal commands`
   ```bash
   appium driver install xcuitest
   appium driver install uiautomator2
   ```

7. Install [IntelliJ IDEA Community](https://www.jetbrains.com/idea/download/#section=mac) and launch.
   1. At the time of writing this, the IntelliJ installer in Publix Self Service is out of date. Please use the link above to install it until a fix is pushed.
8. Install cucumber and gherkin plugin in intelliJ.
   1. Open intelliJ and go to the option `IntelliJ -> Settings -> Plugins`
   2. Select the "Marketplace" tab
   3. Search and install the following plugins **Cucumber for Java** and **Gherkin**
9. Install [Appium Inspector](https://github.com/appium/appium-inspector) (Optional)

### Automatic Setup (Publix-issued Intel MacBooks only):
1. Download the `AutomationInstallScript.sh` file from this repo
2. Open terminal and `cd` to the directory of the installer
3. Enter the command `chmod u+x ./AutomationInstallScript.sh`. This makes the script executable
4. Run the script with `./AutomationInstallScript.sh`
5. As of writing this, the IntelliJ installer from Publix Self Service does not work. Please refer to the point "7" and "8" of the previous section for the instructions in how to install IntelliJ and its plugins.

#### Charles proxy configuration (optional) 
1. Install [Charles Proxy](https://www.charlesproxy.com/download/) (Optional)
2. Open Charles and activate the product (ask your manager for the product key)
3. In Charles, navigate to `Tools > Rewrite` and check the "Enable Rewrite" button.
4. Click the import button and open the `Akamai Bypass.xml` file in the projects `readme_supporting_files` folder. Make sure the akamai bypass rule set is enabled, then click okay to apply the rewrite settings.

## Getting Started

IntelliJ has an official Azure plugin that can be installed for easy access to the repo. Setup instructions can be found [here](https://docs.microsoft.com/en-us/azure/developer/java/toolkit-for-intellij/sign-in-instructions).

If you don't want to use the Azure plugin, the repo can be manually cloned with this command
```code
git clone https://publixvso.visualstudio.com/DefaultCollection/S0PWEBXX_WebSite/_git/mobile-app-automation.v2
```

Maven sources from `pom.xml` should load automatically. If it doesn't, right click `pom.xml` and select `maven > clean install`

## First Time Repo Clone
Before we can run any tests, we need to clone the repo and set some properties

Clone the repo
In IntelliJ: 
Search for Plugins and click it
Search for Azure Devops and install it
![img.png](readme_supporting_files/img.png)
After installing it, close the plugins window
Click on File -> Highlight New -> Click Project From Version Control
Click the version control dropdown -> Select Azure Devops GIT -> Click Clone
![img_2.png](readme_supporting_files/img_2.png)
You should be prompted to log in to azure. Sign in using your regular credentials.
After signing in you will have a list of repositories to clone. Choose Mobile App Automation
![img_4.png](readme_supporting_files/img_4.png)

# Configuration
The framework can be configured by defining the values on the 
`/mobile-app-automation/src/test/resources/global.properties` file
- *appiumHost* Address in which appium server is running or should be launched
- *appiumPort* Port in which appium server is running or should be launched
- *startAppiumServer* Flag that indicates if the appium server initialization should be done by the framework, if it is set to `false` the framework will try to connect to an appium server instance that should be already running
- *takeScreenshotsOnFailure* Indicates if screenshots should be saved as files on scenario failures
- *nodePath* Location of the nodejs binaries

## Setting up device configurations
To run tests on specific devices/emulators, you must set up a `device.properties` file for each device.
1. Refer to the example file for the device type you are trying to set up (iOS/Android) (Real Device/Simulator).
2. In the `src/test/resources/config/devices/enabled` folder, create a new file for your device.
3. Enter the required information into the file based on the example file.
   1. `deviceName`
      1. `Android Emulator` for emulators, for real devices use the `adb devices -l` command and use the `model` value
      2. For iOS, use the simulators name for simulators (i.e. `iPhone 14 Pro`), and for real devices use the value found on the device at `Settings > General > About > Name`
   2. `platformVersion` - The devices OS version (i.e. `13` for Android 13, `16.2` for iOS 16.2)
   3. `udid`
      1. Android Emulators/Real devices, enter the udid from `adb devices`
      2. iOS Simulators/Real devices, enter the udid from `xcrun xctrace list devices`
         1. This list can get pretty big, you may want to grep the output to search for the device you need
         2. `xcrun xctrace list devices | grep "iPhone 14 Pro"`
   4. `platformName` - `iOS` or `Android`
   5. `pcomUsername` - The username for the publix account to be used
      1. You will need to create an account for each device using the format `app_automation_[udid]@mailinator.com`
      2. Since Android emulators use a generic udid, use the format `app_automation_[tester initials]_[udid]@mailinator.com`
   6. `pcomPassword` - The password for the publix account to be used
      1. use `apptest123`
   7. `serviceEnvironment` - The publix.com lifecycle to point to. If not specified "Production" (PRD) will be used by default
      1. Only specify this if you need to point to a lower lifecycle. Use `TST` for test, and `STG` for stage
   8. `systemPort` (Optional when running the scripts in a single device, required when running tests in parallel). Value to specify the WDA port or the UIAutomator2 port, valid values are open ports between 8100 and 65535

To enable/disable a device for execution, simply move the device files between the "enabled" and "disabled" folders. Only device configurations found in the `enabled` folder will be used.

### iOS Real Device specific configuration
In order to run tests on real iOS devices, we must create a `xcodeProperties.xcconfig` file that will be used to sign the WebDriverAgent.

1. Copy `src/test/resources/config/examples/xcodeProperties.xcconfig.EXAMPLE` to `src/test/resources/config/xcodeProperties.xcconfig` 
2. Open `~/.appium/node_modules/appium-xcuitest-driver/node_modules/appium-webdriveragent/WebDriverAgent.xcodeproj` in Xcode
3. On the project root, select the `WebDriverAgentRunner` target.
4. Set your team and check the `Automatically manage signing` box
5. Note the information from the signing certificate section.
   1. `CODE_SIGN_IDENTITY: Dev Name (DEVELOPMENT_TEAM)`
6. Navigate to the `xcodeProperties.xcconfig` file you create in Step 1 and enter that information into the file

## Keeping your local repo up to date
Now that you have completed all the first time set up, you can easily keep your local copy of the project up-to-date
Be on the `main` branch, click update
You will see it fetch and possibly rebuild the project, and then, you should be updated and ready to run the latest automation tests

## Running Tests
By default, tests will execute in the production lifecycle. This can be changed in the device config file by specifying a valid value for the `serviceEnvironment` property (instructions in the device property example files). We should use the latest release candidate build for testing.

The latest release candidate build should be placed under `src/test/resources/app` for the framework to install and run on the desired device.

**We have been asked to no longer place ISPU orders in productions. In order to run these test, we must drop to a lower lifecycle.**

Once you have your device setup correctly, it's time to execute the tests. There are multiple ways to run the scripts

### Running tests using Ad hoc runners for regression testing
In this way the scenarios can be executed targeting a specific platform (Android, iOS).

1. Open the runner file at `src/test/java/cucumber/{Desired Platform}Runner.java`.
2. Right-click on the file and click *`Run '{Desired Platform}Runner'`*.

This will create an intelliJ "configuration run" that can be customized to specify additional arguments.

**Limiting the amount of threads to use.** Edit the "TestRunner" configuration file and on the "Test runner params" specify the value `-dataproviderthreadcount X` where "X" is the number of threads to be used. Make sure that this value is less or equal to the number of `.properties` files located in the `enabled` folder

**Run tests by tag** 
- Edit the file `src/test/resources/cucumber.properties` and set the `cucumber.filter.tags` with the tags expression to filter the scenarios. For further information in how to use the tags for filtering, please refer to the official [cucumber documentation](https://cucumber.io/docs/cucumber/api/?lang=java#running-a-subset-of-scenarios)
![img_2.png](readme_supporting_files/test-runner-config.png)
- This can also be done by editing the "tags" field inside the `@CucumberOptions` annotation available on each platform runner

### Re-running failed scenarios
After having run the scenarios by following the instructions above there may be cases in which one or more
scenarios fail, for running those scenarios again you can run the class `src/test/java/cucumber/RetriesTestRunner.java` in the same way you did with the platform runners

By doing that the framework will run the failed scenarios using the same configuration (devices & platform) used for the original execution.

### Running scenarios or features
In this way you can select a given scenario or "feature" file to be executed

1. Open the ".feature" you want to execute or that contains the needed scenario.
2. Click on the green arrow located to the left of the feature or scenario
   ![img_2.png](readme_supporting_files/run-feature-or-scenario.png)
3. This will create an IntelliJ "Run configuration" and will start the script execution

**Run tests by tag** Edit the file `src/test/resources/cucumber.properties` and set the `cucumber.filter.tags` with the tags expression to filter the scenarios. For further information in how to use the tags for filtering, please refer to the official [cucumber documentation](https://cucumber.io/docs/cucumber/api/?lang=java#running-a-subset-of-scenarios)
**Note** This approach cannot be used to run the scenarios in parallel. In this case if there are multiple `.properties` files in the `enabled` folder, the framework will select the first one in alphabetical order

### Running tests via CLI (using maven)
In this way the scenarios can be run in parallel and specifying the parameters supported by JUnit and cucumber.
The number of threads to be used can be specified using the parameter "threadCount".
When executed in parallel mode each Feature (including all its scenarios) will be run on an arbitrary device.

For running the framework with maven first it is needed to install the subprojects using the following commands
```shell
mvn install -DskipTests
mvn install -pl publix-api-helpers -DskipTests
```

Actually running the framework
```shell
mvn test -pl mobile-app-automation -DthreadCount=<number_of_devices>
```

The command above accepts additional arguments to define the behavior of cucumber and JUnit, for mode information please refer to [Running a subset of scenarios](https://cucumber.io/docs/cucumber/api/?lang=java#running-a-subset-of-scenarios)

Examples
```shell
#Overriding the features folder
mvn test -pl mobile-app-automation -Dcucumber.feature="src/test/resources/features"
```

```shell
#Filtering the scenarios to be executed by using tags
mvn test -pl mobile-app-automation -Dcucumber.filter.tags="@GuestExperience"
```
## Making changes/checking out a branch
When we need to make code changes, we need to start a new branch and make changes on it, then submit a pull request for review.
In the bottom left of IntelliJ, click Git -> right click main (the main branch) and click checkout.
![img_7.png](readme_supporting_files/img_7.png)
Name the branch users/_pnumber/_PBInumber_somethingdescriptive_  
You can now make changes to the project.
**Note** Any uncommitted changes are carried over to any branch you select. So if for some reason you need to switch to
a different branch before you submit your pull request, be sure to commit the changes first
You can switch branches by clicking on your current branch in the bottom right of IntelliJ -> then click on a branch
![img_8.png](readme_supporting_files/img_8.png)

## Page Objects

We use Page Factory to create page objects in our tests. Page Objects are abstractions for the UI elements that you interact with in your tests. 
You can use the `@AndroidFindBy` and `@iOSXCUITFindBy` annotations for each element that you need to access. 
Using these, you can create convenient methods like `clickViewsButton()` which
allow you to write more concise tests.

### Page Object Example

```java
package appium.android.pages;

import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.PageFactory;

public class ExamplePage extends BasePage{

   public ExamplePage(DriverManager driverMgr) {
      super(driverMgr);
   }

   @AndroidFindBy(uiAutomator = "new UiSelector().textContains(\"Home\")")
   @iOSXCUITFindBy(iOSClassChain = "**/XCUIElementTypeStaticText[`label == \"Home\"`]")
   private WebElement homeTitle;

    public boolean isTitleDisplayed() {
       return isElementDisplayedImmediately(guestLoginButton);
    }
}
```

### Scenario Example

```gherkin
Scenario Outline: User logs in successfully
Given This is a fresh install of the app
When The user logs in with "<username>" and "<password>"
Then Verify the user is logged into the app
Examples:
| username | password |
| gkautomation1@mailinator.com | gktest123 |
```
### Appium Inspector
To find the ID of items, we use the Appium Inspector tool. It allows you to connect to a device, and get all the elements that are on the screen.
1. Open terminal and start a new Appium server session using the command `appium server`
2. Open Appium Inspector and enter the information in the device.properties file that you want to connect to (platform version, device name, udid, ect.)
3. Click "Start Session"
4. Navigate to the item you want to get the ID for on the device
5. Refresh the screen in appium inspector and note down the id of the element.
6. Reference this ID in code when creating the `WebElement` object for the element.
7. Sometimes an element will only have a xpath and no stable way to reference it. In these cases, please refer to the steps in the "Elements Without IDs" section of this file.

## Creating a pull request
Once all your changes are done, and you are ready for them to go into main, we submit a pull request for testers to approve
before it can be merged in.

1. Commit all your changes (be sure to include a PBI number and some explanation of the changes when committing)
2. Right-click on your branch -> click Push -> Review the changes intelliJ detected -> click Push. 
3. Navigate to azure devops repo and go to the pull requests screen 
4. Click new pull requests 
5. Fill out the request with appropriate information that the template asks for 
6. Add the `Mobile App Automation` group as a required reviewer 
7. Like the PR to the board work item and submit it

## CI examples

//TODO

## Reporters

[Extent Reports](https://www.extentreports.com/) is utilized to create distributable test analytics, these reports are automatically generated when the scripts
are executed by using the `src/test/java/cucumber/TestRunner.java`. The resulting HTML files can be found under the folder `test-results` and they contain
the summary and detailed information for the scenarios that were executed, in addition if the scenario failed, a screenshot will be added.

**Note:** The HTML Report is not generated when the scripts are directly executed from the `.feature` file.


## Additional Info
### Wiki Location
The wiki for this codebase is contained in the [AppTestAutomationWiki](https://publixvso.visualstudio.com/DefaultCollection/S0PWEBXX_WebSite/_git/AppTestAutomationWiki) repo.

### Elements Without IDs
Sometimes you will encounter an element in the app that does not have any guaranteed way to reference it (weak references). When this happens, follow these steps:
1. Open the [Documenting Missing IDs](https://publixvso.visualstudio.com/DefaultCollection/S0PWEBXX_WebSite/_git/AppTestAutomationWiki?path=/Documenting-Missing-IDs.md&_a=preview) page of the app automation wiki and follow its steps.
2. In the code, create the element using the weak references
   1. Leave a comment next to the `@FindBy` with the ticket number you created during step 1
3. When using that element in code, keep any unstable/workaround logic in its own method at the bottom of the document.
4. Add `WORKAROUND` to the method name (e.g. `clickSomeButtonWORKAROUND()`)
5. Comment the ticket number next to the method with a brief description about why this method was needed.
