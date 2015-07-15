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
