# Data Access

Access to folders and files on the Meerkat cluster is managed by linux groups.

If you want to share data with another user or a group of users the directory containing the data must have group permissions enabled. By default, a user's home directory will only have read and write permissions enabled for the user.

If the data is sensitive and only certain users should have access, then a unique project group should be created which includes all the relevant project members. Once this is done the directory group id or `gid` should be changed to the project group and group permissions can be enabled. Please contact administors to set up projects and project groups.