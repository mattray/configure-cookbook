Configure Cookbook
==========================
Proof of concept cookbook to dynamically change the run list of a node based on the node's attributes (in this case the number of CPUs).

Requirements
------------
Only tested on Ubuntu 14.04.

Usage
-----
#### configure::default

Include `configure::default` in your node's `run_list` and it will evaluate the number of CPUs and change the run list accordingly. On the next chef-client run the `run_list` will no longer include the `default` recipe.

Example
-------
Here's how the cookbook behaves.

```bash
$ knife node run_list set ubuntu1-1404 configure::default
ubuntu1-1404:
  run_list: recipe[configure::default]
mray@farnsworth[23:03]SYSTEM(master)~/ws/runlist-repo/cookbooks
$ knife ssh 'name:ubuntu1-1404' 'sudo chef-client' -a ipaddress
192.168.142.173 knife sudo password:
Enter your password: ********

192.168.142.173
192.168.142.173 Starting Chef Client, version 12.4.1
192.168.142.173 resolving cookbooks for run list: ["configure::default"]
192.168.142.173 Synchronizing Cookbooks:
192.168.142.173   - configure
192.168.142.173 Compiling Cookbooks...
192.168.142.173 Converging 0 resources
192.168.142.173
192.168.142.173 Running handlers:
192.168.142.173 Running handlers complete
192.168.142.173 Chef Client finished, 0/0 resources updated in 8.924944161 seconds
mray@farnsworth[23:04]SYSTEM(master)~/ws/runlist-repo/cookbooks
$ knife node show ubuntu1-1404
Node Name:   ubuntu1-1404
Environment: _default
FQDN:        ubuntu1-1404.vm
IP:          192.168.142.173
Run List:    recipe[configure::b]
Roles:
Recipes:     configure::default
Platform:    ubuntu 14.04
Tags:
mray@farnsworth[23:04]SYSTEM(master)~/ws/runlist-repo/cookbooks
$ knife ssh 'name:ubuntu1-1404' 'sudo chef-client' -a ipaddress
192.168.142.173 knife sudo password:
Enter your password: ********

192.168.142.173
192.168.142.173 Starting Chef Client, version 12.4.1
192.168.142.173 resolving cookbooks for run list: ["configure::b"]
192.168.142.173 Synchronizing Cookbooks:
192.168.142.173   - configure
192.168.142.173 Compiling Cookbooks...
192.168.142.173 Converging 1 resources
192.168.142.173 Recipe: configure::b
192.168.142.173   * log[B log] action write[2015-07-14T23:04:32-05:00] WARN: run list includes recipe[configure::b] and there is 1 CPU
192.168.142.173
192.168.142.173
192.168.142.173
192.168.142.173 Running handlers:
192.168.142.173 Running handlers complete
192.168.142.173 Chef Client finished, 1/1 resources updated in 5.424259504 seconds
mray@farnsworth[23:04]SYSTEM(master)~/ws/runlist-repo/cookbooks
$ knife node show ubuntu1-1404
Node Name:   ubuntu1-1404
Environment: _default
FQDN:        ubuntu1-1404.vm
IP:          192.168.142.173
Run List:    recipe[configure::b]
Roles:
Recipes:     configure::b
Platform:    ubuntu 14.04
Tags:
```

Contributing
------------
1. Fork the repository on GitHub
2. Create a named feature branch (like `add_component_x`)
3. Write you change
4. Write tests for your change (if applicable)
5. Run the tests, ensuring they all pass
6. Submit a Pull Request using GitHub

License and Authors
-------------------

Author:: Matt Ray <matt@chef.io>

Copyright:: 2015 Chef Software, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
