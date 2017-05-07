# vRealize Automation - NSX Integration

NSX integration in vRealize Automation can help creating and configuring existing networks, on-demand NAT networks and on-demand routed networks, creating load balancers, and adding and configuring security groups and security tags for vSphere machines.

## Available Use Cases

### Manage Network Profiles

Import "vRA Samples - Network Profiles.postman_collection.json" in Postman

 * CRUD on network profiles
 * Create external network profiles
 * Create NAT network profiles
 * Create Routed network profiles

### NSX Provisioning Setup

Import "vRA Samples - NSX Provisioning Configuration.postman_collection.json"

### Endpoint

 * Create vSphere endpoint
 * Create NSX endpoint with vSphere endpoint association

#### Network Profiles

 * Create external network profile
 * Create NAT network profile
 * Create Routed network profile

#### Reservation

 * Get reservation networks to select in reservation
 * Get reservation routed gateway to select in reservation
 * Get security group to select in reservation
 * Create vSphere reservation with NSX components

#### Import Blueprints

 * Import blueprints (samples in /resources folder, import only .zip folder)


NOTE: All these methods have variable names defined in the format of {{variable-name}}. Make sure to replace them before calling the method.

*[vRealize Automation API Tips](../API%20Tips)*