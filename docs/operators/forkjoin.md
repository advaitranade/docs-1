import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Fork/Join Task

```json
"type" : "FORK_JOIN"
```

A Fork operation lets you run a specified list of tasks or sub-workflows in parallel. A fork task is followed by a join operation that waits on the forked tasks or sub-workflows to finish. The `JOIN` task also collects outputs from each of the forked tasks or sub workflows.

## Configurations

* A `FORK_JOIN` task has a `forkTasks` attribute that expects an array. Each array is a sub-list of tasks. Each of these sub-lists is then invoked in parallel. The tasks defined within each sublist can be sequential or any other way as desired.
* A FORK_JOIN task has to be followed by a JOIN operation. The `JOIN` operator specifies which of the forked tasks to `joinOn` (waits for completion) before moving to the next stage in the workflow.

### Input Parameters

| Attribute |  Description |
| -- | -- |
| forkTasks | A list of tasks. Each of the outer lists will be invoked in parallel. The inner list can be a graph of other tasks and sub-workflows. |

### Output Parameters

| Attribute |  Description |
| -- | -- |
| joinOn | This is the output configuration of the JOIN task used in conjunction with the FORK_JOIN task. The output of the JOIN task is a map, where the keys are task reference names of the tasks being joined, and the keys are the corresponding outputs of those tasks. | 

:::info Join Task
Check [JOIN](https://orkes.io/content/docs/reference-docs/join-task) for more details on the JOIN aspect of the FORK.
:::

## Examples

<Tabs>
<TabItem value="JSON" label="JSON">

```json
[
  {
    "name": "fork_join",
    "taskReferenceName": "my_fork_join_ref",
    "type": "FORK_JOIN",
    "forkTasks": [
      [
        {
          "name": "process_notification_payload",
          "taskReferenceName": "process_notification_payload_email",
          "type": "SIMPLE"
        },
        {
          "name": "email_notification",
          "taskReferenceName": "email_notification_ref",
          "type": "SIMPLE"
        }
      ],
      [
        {
          "name": "process_notification_payload",
          "taskReferenceName": "process_notification_payload_sms",
          "type": "SIMPLE"
        },
        {
          "name": "sms_notification",
          "taskReferenceName": "sms_notification_ref",
          "type": "SIMPLE"
        }
      ],
      [
        {
          "name": "process_notification_payload",
          "taskReferenceName": "process_notification_payload_http",
          "type": "SIMPLE"
        },
        {
          "name": "http_notification",
          "taskReferenceName": "http_notification_ref",
          "type": "SIMPLE"
        }
      ]
    ]
  },
  {
    "name": "notification_join",
    "taskReferenceName": "notification_join_ref",
    "type": "JOIN",
    "joinOn": [
      "email_notification_ref",
      "sms_notification_ref"
    ]
  }
]
```
</TabItem>
<TabItem value="Java" label="Java">
This is a banana 🍌
</TabItem>
<TabItem value="Golang" label="Golang">
    This is a banana 🍌
</TabItem>
<TabItem value="Python" label="Python">
  This is a banana 🍌
</TabItem>
<TabItem value="CSharp" label="CSharp">
  This is a banana 🍌
</TabItem>
<TabItem value="javascript" label="Javascript">
    This is a banana 🍌
</TabItem>
<TabItem value="clojure" label="Clojure">
    This is a banana 🍌
</TabItem>
</Tabs>

<details><summary>Sending Notifications</summary>
<p>
Imagine a workflow that sends three notifications: email, SMS, and HTTP. Since none of these steps depend on the others, they can be run in parallel with a fork.
The diagram will appear as follows:

![fork diagram](/img/fork-task-diagram.png)

Here's the JSON definition for the workflow:

```json
[
  {
    "name": "fork_join",
    "taskReferenceName": "my_fork_join_ref",
    "type": "FORK_JOIN",
    "forkTasks": [
      [
        {
          "name": "process_notification_payload",
          "taskReferenceName": "process_notification_payload_email",
          "type": "SIMPLE"
        },
        {
          "name": "email_notification",
          "taskReferenceName": "email_notification_ref",
          "type": "SIMPLE"
        }
      ],
      [
        {
          "name": "process_notification_payload",
          "taskReferenceName": "process_notification_payload_sms",
          "type": "SIMPLE"
        },
        {
          "name": "sms_notification",
          "taskReferenceName": "sms_notification_ref",
          "type": "SIMPLE"
        }
      ],
      [
        {
          "name": "process_notification_payload",
          "taskReferenceName": "process_notification_payload_http",
          "type": "SIMPLE"
        },
        {
          "name": "http_notification",
          "taskReferenceName": "http_notification_ref",
          "type": "SIMPLE"
        }
      ]
    ]
  },
  {
    "name": "notification_join",
    "taskReferenceName": "notification_join_ref",
    "type": "JOIN",
    "joinOn": [
      "email_notification_ref",
      "sms_notification_ref"
    ]
  }
]
```
>**NOTE:**
There are three parallel 'tines' to this fork, but only two outputs are required for the JOIN to continue. The diagram does draw an arrow from `http_notification_ref` to the `notification_join`, but it is not required for the workflow to continue.

Here is what the output of notification_join will look like. The output is a map, where the keys are the names of task references being joined. The corresponding values are the outputs of those tasks.

```json

{
  "email_notification_ref": {
    "email_sent_at": "2021-11-06T07:37:17+0000",
    "email_sent_to": "test@example.com"
  },
  "sms_notification_ref": {
    "sms_sent_at": "2021-11-06T07:37:17+0129",
    "sms_sent_to": "+1-xxx-xxx-xxxx"
  }
}
```
</p>
</details>

<details><summary>Document Approvals</summary>
<p>

[Document Approvals](https://orkes.io/content/docs/usecases/document_approvals): When multiple approvals can happen at the same time.
</p>
</details>

<details><summary>Hello World</summary>
<p>

[Hello World Codelab](https://orkes.io/content/docs/codelab/helloworld3)
</p>
</details>

<details><summary>Order Fulfillment</summary>
<p>

[Order Fulfillment Codelab](https://orkes.io/content/docs/codelab/orderfulfillment6)
</p>
</details>