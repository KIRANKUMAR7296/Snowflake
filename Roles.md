# `Roles`

### `ACCOUNTADMIN`

- `SECURITYADMIN` + `SYSADMIN`
- Top level Role, 
- Granted only to limited number of users.

### `SYSADMIN`

- Create `warehouses` and `databases` objects. 

### `SECURITYADMIN`

- Manage `users` and `roles`
- Can manage any object grant globally.

### `USERADMIN`

- Dedicated to `users` only.
- Can create `users` and `roles`

### `PUBLIC`

- Automatically granted to every single user.

We can also create own custom roles or hierarchy of roles.
