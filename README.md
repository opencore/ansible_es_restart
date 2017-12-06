Elasticsearch Rolling Restart
=============================

This role can be used to perform a [rolling restart](https://www.elastic.co/guide/en/elasticsearch/reference/current/rolling-upgrades.html) of an Elasticsearch cluster. All cluster hosts will be restarted one after the other with appropriate wait times in between for the cluster to return to green state.

Requirements
------------

A working Elasticsearch cluster with nodes listening at least on localhost is necessary for this role to be able to work.

Role Variables
--------------

**perform_flush**

Default: true
Should a [synced flush](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-synced-flush.html) be performed before initiating the cluster restart? This can be useful to speed up recovery times down during the restart, but will only work cleanly if you can stop any indexing activity in the cluster.


**ignore_failed_flush**

Default: false
Only relevant if _perform_flush_ is enabled. If this is set to _true_ the role will continue with the restart even if the synced flush call failed on a few shards.

**elastisearch_port**

Default: 9200
The port that should be used to communicate with Elasticsearch. If you have different ports per host override this in the host_vars as necessary.

Dependencies
------------

none

Example Playbook
----------------

The following example playbook would apply the role to all hosts of the group elasticsearch in your inventory using default values:

    - hosts: elasticsearch
      roles:
         - opencore.ansible_es_restart


If you can't stop indexing while you perform the restart you will want to ignore failed shards during the synced flush:

    - hosts: elasticsearch
      roles:
         - { role: opencore.ansible_es_restart, ignore_failed_flush: true }


License
-------

Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to You under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Author Information
------------------

Sönke Liebau is one of the founders of [OpenCore](http://www.opencore.com) , a german company that specialises in open source and big data consulting.

He has been working with Elasticsearch since version 0.20 and uses Ansible for pretty much anything he does.
