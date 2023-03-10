# Zephyr Scale and Robot Framework integration

This is an example project that demonstrates how to configure Robot Framework to generate the JUnit XML results file required for uploading test results to Zephyr Scale using the API [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions).

## Configuration

No configuration is required beforehand. Check the section below to see how to execute tests and upload the test results to Zephyr Scale.

## Executing tests and uploading results to Zephyr Scale

In order to instruct Robot Framework to generate the JUnit XML results file, all that is required is to execute the tests with `-x` parameter followed by the xml file name. Here is an example:

```
robot -x junitresult.xml mytest.robot
```

The command line above will execute the `mytest.robot` test file and generate the JUnit XML results file `junitresult.xml`. Then, this file containing the test results can be uploaded to Zephyr Scale using the following API endpoint: [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions).

The abovementioned API accepts either a single XML file as well as a .zip file containing multiple XML files. The POST request will create a new test cycle in Zephyr Scale containing the results and will respond with the key of the created test cycle.

## Naming conventions

There are 2 ways to link Robot Framework test cases with Zephyr Scale test cases:
- **Zephyr Scale test case key**: in case your Robot framework test case contains the Zephyr Scale test case key
- **Zephyr Scale test case name**: if your Robot Framework test case doesn't contain some Zephyr Scale test case key, then it will try to match Zephyr Scale test case by name using the following pattern `<robot filename with no extension>.<robot test case name>`

Here is an example. Consider a file named `calculator.robot`:
```robotframework
*** Test Cases ***
# will match Zephyr Scale test case named Calculator.User can clear the display
User can clear the display
    Input number    10
    Press operator    +
    Input number    1
    Press clear 
    Display should be empty

*** Test Cases ***
# will match Zephyr Scale test case with key NET-T1743
NET-T1744 User can calculate with wrong result 
    Input number    1
    Press operator    +
    Input number    1
    Press enter 
    Result should be     3

*** Test Cases ***
# will match Zephyr Scale test case with key NET-T1744
User can calculate two numbers - NET-T1744
    [Template]    Calculate two numbers should pass
    10    +    5    15
    10    -    5    5
    10    /    5    2
    10    *    5    50
```
As we can see, the first Robot Framework test cases will match Zephyr Scale test cases by name and the last 2 will match by key.

## Requirements to run this example project

In order to execute this example on your local machine you will have to checkout this repository and install python 3:

```
brew upgrade pyenv
pyenv install 3.6.0
pyenv global 3.6.0
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
```

Now, install Robot Framework and docutils library:

```
pip install robotframework
pip install docutils
```

## More information

For more information, please head to our [documentation page](https://support.smartbear.com/zephyr-scale) or get in [touch with us](https://smartbear.atlassian.net/servicedesk/) if you have any issues or need help.
