# Role-Based Access Check

## Problem

Implement a function that checks if a user has sufficient permissions to perform a specific action, based on their assigned roles.

## Solution

We can define a set of permissions for each role. When an access check is requested, we compare the required permission against the user's roles' permissions.

```javascript
const rolePermissions = {
  admin: ['create', 'read', 'update', 'delete', 'manage_users'],
  editor: ['create', 'read', 'update'],
  viewer: ['read']
};

/**
 * Checks if a user (identified by their roles) has a specific permission.
 * @param {Array<string>} userRoles - An array of roles assigned to the user.
 * @param {string} requiredPermission - The permission needed for the action.
 * @returns {boolean} - True if the user has the required permission, false otherwise.
 */
function hasPermission(userRoles, requiredPermission) {
  if (!userRoles || userRoles.length === 0) {
    return false;
  }

  for (const role of userRoles) {
    const permissions = rolePermissions[role];
    if (permissions && permissions.includes(requiredPermission)) {
      return true;
    }
  }
  return false;
}

// Example
const adminUserRoles = ['admin'];
const editorUserRoles = ['editor'];
const viewerUserRoles = ['viewer'];
const guestUserRoles = [];

console.log('Admin can create:', hasPermission(adminUserRoles, 'create')); // true
console.log('Editor can delete:', hasPermission(editorUserRoles, 'delete')); // false
console.log('Viewer can read:', hasPermission(viewerUserRoles, 'read')); // true
console.log('Guest can update:', hasPermission(guestUserRoles, 'update')); // false
console.log('Admin can manage users:', hasPermission(adminUserRoles, 'manage_users')); // true
```
