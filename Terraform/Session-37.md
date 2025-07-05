### Continuation of the previous session
In last session we completed till "Launch-template" now it is the continuation of "Auto-scaling"

### Rolling update
- For example we have 4 instances are there now
- 4 new instances should be created and replace the old instances
- How the strategy will be followed here ?
- 1 new instance will create and once it is up, then old instance 1 will be deleted, this can lead to no
  down time.
- Similarly like for 2nd,3rd and 4th instances also
- This whole process we call "instance_refresh" so we used this syntax in the code
- We have many strategies, but rolling is the famous.

### Target deregistration
If 1 instance is handling some requests, and later got terminated due to traffic decrease, then deregistration process will start, for example in a company if a employee got terminated, they cannot relieve him on the spot, they need to complete few formalities like did he completed his pending work or not ? did we settled him, did he serviced notice period or not etc.

### Points to remember
- In launch-template we have version, if we want to release a new version of the catalogue, then new version of
  launch template should also be released, we should not delete the Launch-template and create again.
- After updating new version of launch template, we immediately refresh the "Auto-scaling" so we put this
  "update_default_version" = true in code
- Auto-scaling will not just create instances, it will directly place in the target group and attach the
  instances with the Load balancer
- If you are not aware of what options to give in the code, just try to create a sample resource in the aws
  console, and see what options are required, and same options put in the code by taking from the google, do
  for every resource if you are not aware of.
