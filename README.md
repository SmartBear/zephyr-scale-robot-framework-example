# Example of how to use Robot Framework to generate JUnit result file

Small project to show how to make Robot Framework to generate the JUnit result file that you can [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions)

### How to generate the JUnit result files

You just have to execute Robot Framework with `-x` parameter followed by the xml result file name to instruct it to generate the JUnit result file. For testing purposes, you can clone this project and execute Robot Framework like so:

```
robot -x junitresult.xml calculator.robot
```

This will generate the JUnit result file `junitresult.xml` that you'll [`POST /automations/executions/junit`](https://support.smartbear.com/zephyr-scale-cloud/api-docs/#operation/createJUnitExecutions).