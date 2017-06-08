# vRealize Automation - Health Service

## Available Use Cases (v7.3 only)

**Login**

* Login with full access admin
* Login with normal consumer user

**Configuration**

* Manage a configuration (Create/Get/Delete)

**Test Results**

* Get overall test results
* Get individual test results
* Get latest test execution results
* Get an individual result

The results from above samples will give numerous query spec for different scenarios.

For help in generating query spec for health service, look [here](https://github.com/vmware/xenon/wiki/Introduction-to-Service-Queries)

A sample query for latest test execution:

```
POST /core/health-query-tasks
{
    "taskInfo": {
        "isDirect": true
    },
    "querySpec": {
        "query": {
            "occurance": "MUST_OCCUR",
            "booleanClauses": [{
                "occurance": "MUST_OCCUR",
                "term": {
                    "propertyName": "documentKind",
                    "matchValue": "com:vmware:healthbroker:states:ExecutionServiceState",
                    "matchType": "TERM"
                }
            },
            {
                "occurance": "MUST_OCCUR",
                "term": {
                    "propertyName": "configurationLink",
                    "matchValue": "/health/config/configurations/{{configuration-id}}",
                    "matchType": "TERM"
                }
            }]
        },
        "sortTerm": {
            "propertyName": "startedTimestamp",
            "propertyType": "LONG"
        },
        "sortOrder": "DESC",
        "resultLimit": 1,
        "options": ["TOP_RESULTS",
        "EXPAND_CONTENT",
        "SORT"]
    }
}
```

A sample query for individual result:

```
POST /core/health-query-tasks
{
    "taskInfo": {
        "isDirect": true
    },
    "querySpec": {
        "query": {
            "occurance": "MUST_OCCUR",
            "booleanClauses": [{
                "occurance": "MUST_OCCUR",
                "term": {
                    "propertyName": "documentKind",
                    "matchValue": "com:vmware:healthbroker:states:IndividualTestResultServiceState",
                    "matchType": "TERM"
                }
            },
            {
                "occurance": "MUST_OCCUR",
                "term": {
                    "propertyName": "overallResultsLink",
                    "matchValue": "/health/result/overall-results/{{report-id}}",
                    "matchType": "TERM"
                }
            }]
        },
        "sortTerm": {
            "propertyName": "state",
            "propertyType": "STRING"
        },
        "sortOrder": "DESC",
        "options": ["EXPAND_CONTENT",
        "SORT"]
    }
}
```