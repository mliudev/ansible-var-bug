# ansible-var-bug
Demonstrates an ansible variable resolution bug.

The playbook will demonstrate a bug with ansible variable resolution. The bug
occurs when calling a role that is also a dependency of another role. In the
first invocation of the sub-role no parameters are specified because there are
valid defaults in the sub-role defaults folder. In the main-role which depends
on the sub-role we override the sub-role variable with a main-role variable.

What we expect to happen is that the first call to sub-role from the playbook
executes successfully using its default vars. We also expect to see the
main-role call the sub-role and then run its own tasks. However, an error
happens when running the first sub-role. The error appears to indicate that the
top_level_foo variable which shouldn't be necessary, is undefined. top_level_foo
is a variable in main-role's dependencies which is used to override a sub-role
variable default.
