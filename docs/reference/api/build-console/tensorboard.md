---
title: TensorBoard
---

# TensorBoard

## TensorBoard

* **apiVersion**: tensorstack.dev/v1beta1
* **kind**: TensorBoard
* **metadata** ([*ObjectMeta*:octicons-link-external-16:](https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/object-meta/#ObjectMeta){target=_blank})

    Standard object's metadata. More info: [https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata:octicons-link-external-16:](https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata){target=_blank}.

* **spec** ([*TensorBoardSpec*](#tensorboardspec))

    Specification of the desired behavior of the TensorBoard.

* **status** ([*TensorBoardStatus*](#tensorboardstatus))

    Recently observed status of the TensorBoard.

## TensorBoardSpec

* **runMode** (*string*)

    Specifies the run mode of the TensorBoard, defaults to running. Valid options are running and paused.

* **trainingLogFilesets** (*[]string*)

    trainingLogFilesets is the list of filesets containing training log. 

* **image** (*string*)

    image with tensorboard tool.

* **runMode** (*string*)

    TensorBoard run mode, one of runing or paused. If run mode is paused, tensorboard controller will delete service workload to release resources.

## TensorBoardStatus

Recently observed status of the TensorBoard.

* **phase** (*string*)

    A label for the condition of a tensorboard at the current time. Can be one of Initializing, Running or Paused.

* **pod** (*PodStatus*)

    Defines the observed state of the tensorboard pod.

    *PodStatus* display basic info and phase of a pod.

    * **reference** (*PodReference*)

        Refer to pod.

        * **name** (*string*)

            Name of pod.

        * **uid** (*string*)

            Uid of pod.

    * **phase** (*string*)

        Pod phase.

* **conditions** (*[]TensorBoardCondition*)

    Describe tensorboard states in different conditions.

    *TensorBoardCondition* is an observation of the condition of the TensorBoard.

    * **type** (*string*)

        Type of tensorboard condition.

    * **status** (*string*)

        Status of the condition, one of True, False, or Unknown.

    * **message** (*string*)

        A readable message indicating details about the transition.

    * **lastTransitionTime** (*Time*)

        Last time the condition transitioned from one status to another.

    * **lastProbeTime** (*Time*)

        Last time the condition was probed.
