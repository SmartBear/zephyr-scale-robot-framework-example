# Example of how to use Robot Framework to generate JUnit result file

Small project to show how to make Robot Framework to generate the JUnit result file that you can [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions)

### How to generate the JUnit result files

You just have to execute Robot Framework with `-x` parameter followed by the xml result file name to instruct it to generate the JUnit result file. Here is an example:

```
robot -x junitresult.xml mytest.robot
```

This will execute `mytest.robot` test file and generate the JUnit result file `junitresult.xml` that you'll [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions).


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