---
sidebar_position: 2
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Skip Task from Workflow Execution

Skips a given task execution from a current running workflow.

## API
```
PUT /workflow/{workflowId}/skiptask/{taskReferenceName}
```

When skipped the task's input and outputs are updated from **skipTaskRequest** parameter.

## Client SDK Methods

<Tabs>
<TabItem value="Java" label="Java">

```java
void skipTaskFromWorkflow(String workflowId, String taskReferenceName)
```

</TabItem>
<TabItem value="Golang" label="Golang">

```go
func (e *WorkflowExecutor) SkipTasksFromWorkflow(workflowId string, taskReferenceName string, skipTaskRequest model.SkipTaskRequest) error
```

</TabItem>
<TabItem value="Python" label="Python">

```python
WorkflowResourceApi.skip_task_from_workflow(self, workflow_id, task_reference_name, **kwargs)
```

</TabItem>
<TabItem value="CSharp" label="CSharp">

```csharp
void WorkflowResourceApi.SkipTaskFromWorkflow(string workflowId, string taskReferenceName, SkipTaskRequest skipTaskRequest)
```

</TabItem>
<TabItem value="Javascript" label="Javascript">

```javascript
WorkflowResourceService.skipTaskFromWorkflow(
    workflowId: string,
    taskReferenceName: string,
    requestBody?: SkipTaskRequest,
): CancelablePromise<any>
```

</TabItem>
<TabItem value="Clojure" label="Clojure">

```clojure
(workflow-resource/skip-task-from-workflow [options workflow-id task-reference-name])
```

</TabItem>
</Tabs>