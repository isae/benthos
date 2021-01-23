---
title: sftp
type: output
status: beta
categories: ["Network"]
---

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the contents of:
     lib/output/sftp.go
-->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

BETA: This component is mostly stable but breaking changes could still be made outside of major version releases if a fundamental problem with the component is found.

Sends message parts as objects to a file via an SFTP connection.

Introduced in version 3.36.0.


<Tabs defaultValue="common" values={[
  { label: 'Common', value: 'common', },
  { label: 'Advanced', value: 'advanced', },
]}>

<TabItem value="common">

```yaml
# Common config fields, showing default values
output:
  sftp:
    address: ""
    path: ""
    credentials:
      username: ""
      password: ""
    max_in_flight: 1
    max_connection_attempts: 10
```

</TabItem>
<TabItem value="advanced">

```yaml
# All config fields, showing default values
output:
  sftp:
    address: ""
    path: ""
    credentials:
      username: ""
      password: ""
    max_in_flight: 1
    max_connection_attempts: 10
    retry_sleep_duration: 5s
```

</TabItem>
</Tabs>

In order to have a different path for each object you should use function
interpolations described [here](/docs/configuration/interpolation#bloblang-queries), which are
calculated per message of a batch.

## Performance

This output benefits from sending multiple messages in flight in parallel for
improved performance. You can tune the max number of in flight messages with the
field `max_in_flight`.

## Fields

### `address`

The address of the server to connect to that has the target files.


Type: `string`  
Default: `""`  

### `path`

The file to save the messages to on the server.


Type: `string`  
Default: `""`  

### `credentials`

The credentials to use to log into the server.


Type: `object`  

### `credentials.username`

The username to connect to the SFTP server.


Type: `string`  
Default: `""`  

### `credentials.password`

The password for the username to connect to the SFTP server.


Type: `string`  
Default: `""`  

### `max_in_flight`

The maximum number of messages to have in flight at a given time. Increase this to improve throughput.


Type: `number`  
Default: `1`  

### `max_connection_attempts`

How many times it will try to connect to the server before exiting with an error.


Type: `number`  
Default: `10`  

### `retry_sleep_duration`

How long it will sleep after failing to connect to the server before trying again, defaults to 5s if not provided.


Type: `string`  
Default: `"5s"`  

```yaml
# Examples

retry_sleep_duration: 10s

retry_sleep_duration: 5m
```

