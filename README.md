## JQ Questions

* Q1: Pretty-print/format this file: wpl-wrk-int-prd/ap-southeast-2/lambda/list-functions.json (edited

`jq '.' list-functions.json`

* Q2: Print the list of FunctionName from the file: wpl-wrk-int-prd/ap-southeast-2/lambda/list-functions.json


`jq '.Functions[] | .FunctionName' list-functions.json`

* Q3: Count the number of functions in the file: wpl-wrk-int-prd/ap-southeast-2/lambda/list-functions.json

`jq '[.Functions[]] | length' list-functions.json`

* Q4: For every Lambda function that has a Runtime of (exactly) python3.8, print out its FunctionName (source:wpl-wrk-int-prd/ap-southeast-2/lambda/list-functions.json)

`jq '.Functions[] | select(.Runtime == "python3.8").FunctionName' list-functions.json`

* Q5: For every Lambda function that has a Runtime that starts with python (even future versions, don't hardcode a list), print out its FunctionName (source:wpl-wrk-int-prd/ap-southeast-2/lambda/list-functions.json)

`jq '.Functions[] | select(.Runtime|test("python.")).FunctionName' list-functions.json`

* Q6: Assuming you have an environment variable called RUNTIME that contains python3.8 , solve Q4 by using the jq parameter --arg (you are not allowed to cheat and use bash-parameter expansion within the jq-filter.

`jq --arg a "$RUNTIME" '.Functions[] | select(.Runtime == $a) | .FunctionName' list-functions.json`

* Q7: Solve Q5, but rather than operate on a single file, operate on every file as a single stream. Hint, use the jq parameter --slurp. You want something like:
cat wpl-*/*/lambda/list-functions.json | jq -rs 'FILTER'

`jq -s '.[].Functions[] | select(.Runtime|test("python.")).FunctionName' list-functions*.json`
