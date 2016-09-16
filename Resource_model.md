# Resource model

1. Everything is a resource. Simulators, teams, simulations...

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

1. When a resource changes, a websocket notifies each user with permissions to it.

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

* Root resources have permissions, and their data contains the list of fields for the
data in leaves.

* Leaf resources have permissions and may have data.

* Route to read all resources (which user has permission to): `GET /permissions`

* Route to read all leaves of a root: `GET /<root_id>`

* Both routes below return all data and permissions for a resource:

    * `GET /permissions/<resource_id>`

    * `GET /<root_id>/<leaf_id>`

### Update data

* Root resources data is not updatable.

* Leaf resources may have data. The data format will be detailed in its root resource.

* Route: `PUT /<root_id>/<leaf_id>`

### Update permissions

* Route to grant: `POST /permissions/<resource_id>`

* Route to revoke: `DELETE /permissions/<resource_id>`

## Summary of resources and operations

Server | Resource | Root | leaf | Create | Delete | Read | Update data | Grant / revoke
-------|----------|------|------|--------|--------|------|-------------|---------------
**auth** | | | | | | | |
 | group | ✔ | group- | on init | never | GET /permissions/group GET /group | - | POST /permissions/group DELETE /permissions/group
 | group- | group | ✔ | POST /group | DELETE /group/group- | GET /group/group- GET /permissions/group- | POST /group/group- | POST /permissions/group- DELETE /permissions/group-
**portal** | | | | | | | |
 | simulator | ✔ | simulator- | on init | never | GET /permissions/simulator GET /simulator | - | POST /permissions/simulator DELETE /permissions/simulator
 | simulator- | simulator | ✔ | POST /simulator | DELETE /simulator/simulator- | GET /simulator/simulator- GET /permissions/simulator- | POST /simulator/simulator- | POST /permissions/simulator- DELETE /permissions/simulator-

Add all here once the common pattern has been agreed upon.
