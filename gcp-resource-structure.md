
# Resources and Access 

## From bottom to top
- Resources
  - __Q: Can a Resource shared by multiple projects?__ A: No! Each resource belongs to exactly one project.
- Project
  - ID, name, number
- Folder 
  - __Q: Can you have only folders without an organization node?__ A: NO!! A folder MUST belong to a Organization node!!
- Organization node

Note: Usually, policies can not be applied to resources level, i.e. only some Google Clound services allow policies to be applied to individual resources.

## Q: Which tool should I turn to if I want to list/create/update/delete projects in my google account?

A: Google Cloud's Resource Manager tool. Which:
- provides __programmatic__ access to GCP through RPC(Remote Procedure Call) API and REST API
- It can even recover projects that were previously deleted

