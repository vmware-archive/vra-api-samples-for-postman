# vRealize Automation API - Tips

Most of the vRealize Automation APIs are required some sort of authentication token. They also support paging, sorting and filtering.

## Available Use Cases

### Login

```
POST https://{{va-fqdn}}/identity/api/tokens
Accept: application/json
Content-Type: application/json
Request Body:
{
	"username":"{{username}}",
	"password":"{{password}}",
	"tenant":"{{tenant}}"
}

```

### Pagination

```
https://{{va-fqdn}}/reservation-service/api/reservations?page={{page}}&limit={{limit}}
```

Each GET call (that returns list) will return metadata in the following format:

```
"metadata": {
    "size": 20, // default page limit defined by {{limi}}
    "totalElements": 30, // total number of elements across all pages
    "totalPages": 2, // total pages
    "number": 1, // page number
    "offset": 0
  }
```

### Sorting

```
https://{{va-fqdn}}/reservation-service/api/reservations?orderBy=name+desc
```

### Filter

```
https://{{va-fqdn}}/reservation-service/api/reservations?$filter=name eq '{{reservation-name}}'
```

**Available OData Filters**

```
SUPPORTED:
* eq - Equal - /suppliers?$filter=address/city eq 'Palo Alto'
* ne - Not equal - /suppliers?$filter=address/city ne 'San Francisco'
* gt - Greater than - /products?$filter=price gt 20
* ge - Greater than or equal - /products?$filter=price ge 10
* lt - Less than - /products?$filter=price lt 20
* le - Less than or equal - /products?$filter=Price le 100
* and - Logical and - /products?$filter=Price le 200 and Price gt 3.5
* or - Logical or - /products?$filter=Price le 3.5 or Price gt 200
* not - Logical negation - /products?$filter=not endswith(description,'milk')
* ( ) - Precedence grouping - /products?$filter=(city eq 'Palo Alto' or city eq 'San Francisco') and price ge 10
* startswith - /customers?$filter=startswith(companyName, 'VMw')
* endswith - /customers?$filter=endswith(companyName, 'ware')
* substringof - /customers?$filter=substringof('Mwa', companyName)
* length - customers?$filter=length(companyName) gt 5
* tolower - customers?$filter=tolower(companyName) eq 'vmware'
* toupper - customers?$filter=tolower(companyName) eq 'VMWARE'

NOT SUPPORTED: 
* replace
* any Arithmetic operations defined by OData specifications - add, sub, mul, div, mod ...
```

**Catalog Service Filter**

Some catalog-service domain models contain nested objects ending in 'Ref' (which denotes the nested object is a reference to an object rather than a full-blown nested object). When crafting your $filter query, you must remove 'Ref'. Also, each 'Ref' object contains an id and sometimes a label. When attempting to filter on these fields, you must use OData resources of id and name (respectively).

Here's an example to make things clearer. Let's say you want to see all consumer catalog items that are associated with a specific catalog service name. 

Note: Notice how even though the serviceRef object contains a label element, we use service (and not serviceRef) and name (and not label) to craft the filter: $filter=service/name eq 'theName'

```
https://{{va-fqdn}}/catalog-service/api/consumer/catalogItems?$filter=service/name+eq+'{{service-name}}'
```

