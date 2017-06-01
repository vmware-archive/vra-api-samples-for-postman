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

This is what a sample result look like:

```
{
  "testMethod": { 
    "name": "vRealize Automation Node Common Name Certificate Check", 
    "description": "This test case verifies that the vRA node certificate Common names match that of it's server. This test is most useful for distributed/HA environments.",
    "descriptionType": "text",
    "severity": "CRITICAL",
    "methodName": "areVraNodeCertsCommonNameValid", 
    "accessLevel": "INFRASTRUCTURE",
    "enabled": false,
    "configurationReferences": []
  },
  "startTime": "1478213951731",  
  "endTime": "1478213960684", 
  "state": "FAILED", 
  "message": "Not all checks were successful. See the following errors for more details: \njava.io.IOException: Unable to get the certificate of your server [{{va-fqdn}}:443]. Please confirm configuration information. The returned exception is: [java.net.UnknownHostException: {{va-fqdn}}] \n", 
  "remediationType": "html",
  "remediation": "http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2106583", 
  "overallResultsLink": "/health/result/overall-results/Report_vRA_20161103-22.59.03.0373", 
}
```