# vRealize Automation - Approval Service

The approval service provides features for managing and tracking the human approval tasks associated with a service process/artifact in a provider realm. It also provides a record of the approval process when it completes.

## Available Use Cases

### Configuration

The following samples will help in creating new approval policy.

 * Get approval policy types
 * Define and create approval policy

 A typical payload to create a basic approval policy for policy type "Service Catalog - Catalog Item Request" will look like below:

 ```
 POST https://{{va-fqdn}}/approval-service/api/policies

 {
  "name": "{{approval-policy-name}}",
  "description": "",
  "policyType": {
    "id": "com.vmware.cafe.catalog.request.catalogitem",
    "name": "Service Catalog - Catalog Item Request",
    "description": "",
    "serviceTypeId": "com.vmware.csp.core.cafe.catalog",
    "classId": "catalogItemRequest",
    "typeFilter": null,
    "phaseTypes": [
      {
        "id": "com.vmware.cafe.catalog.request.pre",
        "name": "Pre Approval",
        "description": "Approvals sought before a request is fulfilled.",
        "forms": null,
        "phaseOrder": 0,
        "allowUpdates": true
      },
      {
        "id": "com.vmware.cafe.catalog.request.post",
        "name": "Post Approval",
        "description": "Approvals sought after a request has been fulfilled.",
        "forms": null,
        "phaseOrder": 1,
        "allowUpdates": false
      }
    ]
  },
  "state": "PUBLISHED",
  "stateName": "Active",
  "phases": [
    {
      "phasetype": {
        "id": "com.vmware.cafe.catalog.request.pre",
        "name": "Pre Approval",
        "description": "Approvals sought before a request is fulfilled.",
        "forms": null,
        "phaseOrder": 0,
        "allowUpdates": true
      },
      "levels": [
        {
          "name": "Level 1",
          "description": "",
          "approvers": [
            {
              "value": "{{approver-1-username@domain}}",
              "type": "USER",
              "displayName": "{{approver-1-display-name}}"
            },
            {
              "value": "{{approver-2-username@domain}}",
              "type": "USER",
              "displayName": "{{approver-2-display-name}}"
            }
          ],
          "approvalMode": "ANY",
          "criteria": {
            "type": "constantClause",
            "value": {
              "type": "boolean",
              "value": true
            }
          },
          "editSchema": {
            "fields": []
          },
          "levelNumber": 1,
          "external": false
        }
      ],
      "name": "Pre Approval",
      "description": "Approvals sought before a request is fulfilled."
    },
    {
      "phasetype": {
        "id": "com.vmware.cafe.catalog.request.post",
        "name": "Post Approval",
        "description": "Approvals sought after a request has been fulfilled.",
        "forms": null,
        "phaseOrder": 1,
        "allowUpdates": false
      },
      "levels": [
        {
          "name": "Level 2",
          "description": "",
          "approvers": [
            {
              "value": "{{approver-username@domain}}",
              "type": "USER",
              "displayName": "{{approver-display-name}}"
            }
          ],
          "approvalMode": "ANY",
          "criteria": {
            "type": "constantClause",
            "value": {
              "type": "boolean",
              "value": true
            }
          },
          "editSchema": {
            "fields": []
          },
          "levelNumber": 1,
          "external": false
        }
      ],
      "name": "Post Approval",
      "description": "Approvals sought after a request has been fulfilled."
    }
  ],
  "approvableItemId": null,
  "typeFilter": null,
  "approvableItemName": null,
  "approvableItemServiceTypeId": null,
  "createdBy": "{{username}}",
  "version": 0
}
 ```

### Action

The following samples will help perform approval actions programmatically.

 * Get approval work items
 * Get approval request information
 * Approve a request
 * Reject a request

A basic approve request payload will look like as below:

```
POST https://{{va-fqdn}}/workitem-service/api/workitems/{{work-item-guid}}/actions/com.vmware.csp.core.approval.action.approve

{
  "workItemId": "{{work-item-guid}}",
  "workItemActionId": "com.vmware.csp.core.approval.action.approve",
  "formData": {
    "entries": [
    	{
			"key": "source-source-provider-Cafe.Shim.VirtualMachine.NumberOfInstances",
			"value": {
				"type": "integer",
				"value": 1
			}
    	},
    	{
			"key": "source-source-provider-VirtualMachine.Memory.Size",
			"value": {
				"type": "integer",
				"value": 512
			}
    	},
    	{
			"key": "source-source-provider-VirtualMachine.CPU.Count",
			"value": {
				"type": "integer",
				"value": 1
			}
    	},
    	{
			"key": "source-source-provider-VirtualMachine.LeaseDays",
			"value": {
				 "type": "integer",
				 "value": 0
			}
		},
    	{
			"key": "source-businessJustification",
			"value": {
				 "type": "string",
				 "value": "{{business reason}}"
			 }
		}
    ]
  }
}
```

*[vRealize Automation API Tips](../API%20Tips)*
