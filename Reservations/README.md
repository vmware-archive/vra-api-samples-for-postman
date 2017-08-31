# vRealize Automation - Reservation Service

A reservation is a pool of resources for provisioning, consisting of several different types of resources. For example, a virtual reservation allocates a share of the memory, CPU and storage resources on a particular compute resource for a business group to use. You can use the Reservation Service to manage reservations.

## Available Use Cases

### Reservation

 * Get reservation data such as compute resource, storagePath, networks etc.
 * Create reservation (samples include vSphere and vSphere with NSX component)
 * Edit Reservation: Use the following flow:
   * Get all reservations
   * Get individual reservation by ID, copy the response and paste it in a editor.
   * Remove `createdDate`, `lastUpdated`, `version`, Update other values as required.
   * Call Update reservation sample with updated payload as modified in earlier steps.

### Reservation Policy

 * CRUD on reservation policy
 * CRUD on storage reservation policy

NOTE: A fabric administrator should be able to manage rservation and reservation policies.

*[vRealize Automation API Tips](../API%20Tips)*