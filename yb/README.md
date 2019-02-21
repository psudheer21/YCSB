<!--
Copyright (c) 2015 YCSB contributors. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License"); you
may not use this file except in compliance with the License. You
may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
implied. See the License for the specific language governing
permissions and limitations under the License. See accompanying
LICENSE file.
-->

# YB bindings for YCSB

[YugaByte](http://yugabyte.com) is a cloud-agnostic high-performance data fabric.

## Benchmarking YB

Use the following command line to load the initial data into an existing YB cluster with default
configurations.

```
bin/ycsb load yb -P workloads/workloada
```

Additional configurations:
* `masterQuorum`: The master's address. The default configuration expects a master on localhost.
* `pre_split_num_tablets`: The number of tablets (or partitions) to create for the table. The default
uses 4 tablets. A good rule of thumb is to use 5 per tablet server.
* `table_num_replicas`: The number of replicas that each tablet will have. The default is 3. Should
only be configured to use 1 instead, for single node tests.
* `sync_ops`: If the client should buffer data before sending it. The default is false. Should
always be set to true for the run phase.

Then, you can run the workload:

```
bin/ycsb run yb -P workloads/workloada -p sync_ops=true
```