# helm test working session

- test directory with multiple values files
- testing of image, testing of chart
- on installation all resources can come up
- what if you want to run helm test on production
- do we want different test scenarios where you plugin different values?
- out of bounds usecase: cluster audit, all security requirements are up to date
- what do we want to persist? do we want structured output, be able to trace failures?
- plugin for acceptance testing via a Chart?
- chart validation should be separated from application validation
- need for DSL to validate different values
- need to figure out which personas need testing
- compile-time testing, static analysis testing, dynamic testing

Personas:
1. Does this create valid K8s object?

2. Helm end user

3. Helm Chart developer


Action Items
- create #helm-test slack channel
- develop test personas
