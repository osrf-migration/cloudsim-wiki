# Resource model

1. Everything is a resource. Simulators, groups, simulations...

1. Users can have one of the following permissions to a resource:

    * No permission

    * Read permission

    * Write permission

1. There's no concept of permission inheritance, permissions must be
granted for each resource.

1. A user can only grant or revoke up to its own permissions.

1. There are 5 operations which a user can perform on a resource:

    * Create the resource

    * Delete the resource

    * Read its data and list of users with permissions

    * Update its data

    * Update its permissions (grant / revoke)

1. A user with **read** permission to a resource can perform the following:

    * Read its data and permissions

    * Update its permissions (grant **read** permission to another user)

1. A user with **write** permission to a resource can perform all operations.

1. A resource can be a **root resource** or a **leaf resource**.

1. Having write permission to a **root resource** means a user can
create **leaf resources**.

## Operations

### Create

* Root resources are created at init.

* To create a leaf resource, a user needs **write permission to its root resource**.

* Route: `POST /<root_id>`

### Delete

* Root resources can't be deleted even with write permission.

* To delete a leaf resource, a user needs **write permission to the leaf resource**.

* Route: `DELETE /<root_id>/<leaf_id>`

### Read

* Root resources have permissions but no data.

* Leaf resources have permissions and may have data.

* Route to read permissions: `GET /permissions/<resource_id>`

* Route to read data: `GET /<root_id>/<leaf_id>`

### Update data

* Root resources have no data.

* Leaf resources may have data.

* Route: `PUT /<root_id>/<leaf_id>`

### Update permissions

* Route: `POST /permissions/<resource_id>`



## Summary of resources and operations

Server | Resource | Root | leaf | Create | Delete | Read | Update data | Grant / revoke
-------|----------|------|------|--------|--------|------|-------------|---------------
auth | groups | ✔ | group- | on init | never | GET /permissions/groups | - | POST /permissions/groups
auth | group- | groups | ✔ | POST /groups | DELETE /groups/group- | GET /groups/group- GET /permissions/group- | POST /groups/group- | POST /permissions/group-