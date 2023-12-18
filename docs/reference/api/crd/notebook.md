# API Reference

## Packages
- [tensorstack.dev/v1beta1](#tensorstackdevv1beta1)


## tensorstack.dev/v1beta1

Package v1beta1 contains API Schema definitions for the v1beta1 API group

### Resource Types
- [Notebook](#notebook)
- [NotebookList](#notebooklist)



#### Notebook



Notebook is the Schema for the notebooks API

_Appears in:_
- [NotebookList](#notebooklist)

| Field | Description |
| --- | --- |
| `apiVersion` _string_ | `tensorstack.dev/v1beta1`
| `kind` _string_ | `Notebook`
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[NotebookSpec](#notebookspec)_ |  |
| `status` _[NotebookStatus](#notebookstatus)_ |  |


#### NotebookCondition



NotebookCondition defines the observed condition of notebook

_Appears in:_
- [NotebookStatus](#notebookstatus)

| Field | Description |
| --- | --- |
| `type` _[NotebookConditionType](#notebookconditiontype)_ | Type is the type of the condition. Possible values are `Idle`, etc |
| `status` _[ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#conditionstatus-v1-core)_ | Status is the status of the condition type. Possible values of type Idle are `True|False|Unknown` |
| `message` _string_ | Message is a human-readable message for the reason of the status. |
| `lastTransitionTime` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#time-v1-meta)_ | LastTransitionTime is the last time the status was changed. |
| `lastProbeTime` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#time-v1-meta)_ | LastProbeTime is the last time the condition was probed. |


#### NotebookConditionType

_Underlying type:_ `string`



_Appears in:_
- [NotebookCondition](#notebookcondition)



#### NotebookList



NotebookList contains a list of Notebook



| Field | Description |
| --- | --- |
| `apiVersion` _string_ | `tensorstack.dev/v1beta1`
| `kind` _string_ | `NotebookList`
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `items` _[Notebook](#notebook) array_ |  |


#### NotebookPhase

_Underlying type:_ `string`



_Appears in:_
- [NotebookStatus](#notebookstatus)



#### NotebookRunMode

_Underlying type:_ `string`



_Appears in:_
- [NotebookSpec](#notebookspec)



#### NotebookSSHSpec



NotebookSSHSpec defines the ssh template spec of Notebook

_Appears in:_
- [NotebookSpec](#notebookspec)

| Field | Description |
| --- | --- |
| `enabled` _boolean_ | If true, SSH service will be started for this Notebook instance. |
| `serviceType` _[ServiceType](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#servicetype-v1-core)_ |  |
| `authorized_keys` _string array_ | A list of names of v1.Secret containing SSH public keys authorized for access to this SSH service. |


#### NotebookSSHStatus



NotebookSSHStatus defines the observed state of the SSH service associated with the Notebook.

_Appears in:_
- [NotebookStatus](#notebookstatus)

| Field | Description |
| --- | --- |
| `serviceName` _string_ | The v1.Service name of the SSH service. |
| `port` _integer_ | The port number of the SSH server daemon. |
| `clusterIp` _string_ |  |
| `nodePort` _integer_ |  |
| `protocol` _[Protocol](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#protocol-v1-core)_ |  |
| `lastSshClientActivity` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#time-v1-meta)_ | LastSshClientActivity is the last time an SSH client is active. |


#### NotebookSpec



NotebookSpec defines the desired state of a Notebook.

_Appears in:_
- [Notebook](#notebook)

| Field | Description |
| --- | --- |
| `template` _[NotebookTemplateSpec](#notebooktemplatespec)_ |  |
| `scheduler` _[SchedulePolicy](#schedulepolicy)_ |  |
| `ssh` _[NotebookSSHSpec](#notebooksshspec)_ |  |
| `type` _[NotebookType](#notebooktype)_ |  |
| `runMode` _[NotebookRunMode](#notebookrunmode)_ |  |


#### NotebookStatus



NotebookStatus defines the observed state of a Notebook.

_Appears in:_
- [Notebook](#notebook)

| Field | Description |
| --- | --- |
| `phase` _[NotebookPhase](#notebookphase)_ |  |
| `pod` _[PodStatus](#podstatus)_ |  |
| `ssh` _[NotebookSSHStatus](#notebooksshstatus)_ |  |
| `conditions` _[NotebookCondition](#notebookcondition) array_ | Conditions is an array of current conditions |
| `url` _string_ | The URL to Web UI of the notebook |


#### NotebookTemplateSpec



NotebookTemplateSpec defines the pod template to run a Notebook.

_Appears in:_
- [NotebookSpec](#notebookspec)

| Field | Description |
| --- | --- |
| `spec` _[PodSpec](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#podspec-v1-core)_ |  |


#### NotebookType

_Underlying type:_ `string`



_Appears in:_
- [NotebookSpec](#notebookspec)



#### PodReference



PodReference references a K8s v1.Pod.

_Appears in:_
- [PodStatus](#podstatus)

| Field | Description |
| --- | --- |
| `name` _string_ | Name of the Pod. |
| `uid` _string_ | UID of the Pod. |


#### PodStatus



Pod defines the observed state of the Pod running the notebook.

_Appears in:_
- [NotebookStatus](#notebookstatus)

| Field | Description |
| --- | --- |
| `reference` _[PodReference](#podreference)_ | References to the subordinate v1.Pod. |
| `phase` _[PodPhase](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#podphase-v1-core)_ | Replicated from the corresponding field in the subordinate v1.Pod. |


#### SchedulePolicy



SchedulePolicy specifies the preferred scheduler responsible for handling resource allocation requests.

_Appears in:_
- [NotebookSpec](#notebookspec)

| Field | Description |
| --- | --- |
| `t9kScheduler` _[T9kScheduler](#t9kscheduler)_ |  |


#### T9kScheduler





_Appears in:_
- [SchedulePolicy](#schedulepolicy)

| Field | Description |
| --- | --- |
| `queue` _string_ | Name of the queue to use with the T9kScheduler. |


