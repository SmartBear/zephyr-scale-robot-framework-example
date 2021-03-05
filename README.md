# Example of how to use Robot Framework to generate JUnit result file

Small project to show how to make Robot Framework to generate the JUnit result file that you can [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions)

### Configuration

You just have to execute Robot Framework with `-x` parameter followed by the xml result file name to instruct it to generate the JUnit result file. Here is an example:

```
robot -x junitresult.xml mytest.robot
```

This will execute `mytest.robot` test file and generate the JUnit result file `junitresult.xml` that you'll [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions).


### Naming conventions

There are 2 ways to match Robot Framework test cases with Zephyr Scale test cases:
- **By Zephyr Scale test case key**: in case your Robot framework test case contains the Zephyr Scale test case key
- **By Zephyr Scale test case name**: if your Robot Framework test case doesn't contain some Zephyr Scale test case key, then it will try to match Zephyr Scale test case by name following the pattern `<robot filename with no extension>.<robot test case name>` 

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

### Requirements to run this example project

In order to execute this example on your local machine you’ll have to checkout this repository and install python 3. Here is how you can do it on mac:

```
brew upgrade pyenv
pyenv install 3.6.0
pyenv global 3.6.0
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
```

Now you have to install robot framework and docutils library:

```
pip install robotframework
pip install docutils
```

You can now make Robot Framework to generate the JUnit result file by executing the following command:

```
robot -x junitresult.xml calculator.robot
```