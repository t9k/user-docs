---
title: MPIJob
---

# MPIJob

## MPIJob

MPIJob enables running distributed computing tasks in Kubernetes through using MPI protocol.

* **apiVersion**: batch.tensorstack.dev/v1beta1
* **kind**: MPIJob
* **metadata** ([*ObjectMeta*:octicons-link-external-16:](https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/object-meta/#ObjectMeta){target=_blank})

    Standard object's metadata. More info: [https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata:octicons-link-external-16:](https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata){target=_blank}.

* **spec** ([*MPIJobSpec*](#mpijobspec))

    Specification of the desired behavior of the MPIJob.

* **status** ([*MPIJobStatus*](#mpijobstatus))

    Most recently observed status of the MPIJob.

## MPIJobSpec

MPIJobSpec is the specification of the desired behavior of the MPIJob.

* **worker** (*WorkerConfig*)

    Describes the workers that will be created.

    * **replicas** (*int32*)

        The number of MPI workers. This is a pointer to distinguish between explicit zero and not specified. Default 1.

    * **extraMPIArgs** (*[]string*)

        MPI args.

    * **cmd** (*[]string*), required

        Defines how the workers run.

    * **template** ([*PodTemplateSpec*:octicons-link-external-16:](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-template-v1/#PodTemplateSpec)){target=_blank}

        Template describes the Pods that will be created.

* **mca** (*map[string]string*)

    Open MPI uses Modular Component Architecture(MCA) parameters to provide a way to tune your runtime environment. 

* **ssh** (*SSHConfig*)

    SSH configs

    * **sshAuthMountPath** (*string*)

        SSHAuthMountPath is the directory where SSH keys are mounted. Defaults to "/root/.ssh".

    * **sshdPath** （*string*)

        Sshd abstract path. Default to "/usr/sbin/sshd"

* **runPolicy** (*RunPolicy*)

    Specifies various rules for managing the running of a MPIJob.

    *RunPolicy* encapsulates various runtime policies of the distributed training job, for example how to clean up resources.

    * **cleanUpWorkers** (*string*)

        Clean the tasks after the training job finished, one of "all", "unfinished" or "none".

* **mpiHome** (*string*)

    Tells `mpirun` in which directory.

* **scheduler** (*SchedulerPolicy*)

    Choose the appropriate Scheduler to schedule replicas. Can be Kubernetes Default Scheduler or T9k Scheduler. Default use Kubernetes Default Scheduler.

    *SchedulerPolicy* assign the replicas to a specific scheduler.

    * **t9kScheduler** (*T9kScheduler*)

        T9k Scheduler configuration.

        *T9kScheduler* descibes the PodGroup that will be created.

        * **queue** (*string*), required

            T9k Scheduler Queue name. All T9k Scheduler PodGroups should work in a Queue.

        * **priority** (*int32*)

            Indicates the PodGroup's priority. range is [0,100]. Default 0.

* **runMode** (*RunMode*)

    MPIJob can run in three modes: normal, debug and pause. Normal - run the job; debug - create training environment but not train; pause - keep the GenericJob CR but not create the workload.
    
    *RunMode* tells which mode to use and how the job works in this mode.

    * **debug** (*DebugMode*)

        Describes how the debug mode works.

        * **enable** (*bool*)

            Whether to enable DebugMode, defaults to false.

        * **replicaSpecs** (*[]ReplicaDebugSet*)

            Describe how to start replicas in debug mode.

            *ReplicaDebugSet* describe how to start a replica in debug mode.

            * **type** (*string*), required

                The type of the replica, one of "master" or "worker".

            * **skipInitContainer** (*bool*)

                Whether to skip initContainer.

            * **command** (*[]string*)

                Command which will override the containers of replicaSpecs.

    * **pause** (*PauseMode*)
   
        *PauseMode* describes how the debug mode works.

        * **enable** (*bool*)

            Whether to enable pause mode, defaults to false.

        * **resumeSpecs** (*[]ResumeSpec*)

            Describe how to resume replicas from pause mode.

            *ResumeSpec* describe how to restart replicas from pause mode.

            * **type** (*string*), required

                The type of the replica, one of "master" or "worker".

            * **skipInitContainer** (*bool*)

                Whether to skip initContainer.

            * **command** (*[]string*)

                Command to execute in the replica. Use spec.replicaSpecs.template.container.command by default.

            * **args** (*[]string*)

                Command args. Use spec.replicaSpecs.template.container.command by default.

## MPIJobStatus

MPIJobStatus is the most recently observed status of the MPIJob.

* **phase** (*string*)

    Defines all possible phases of training, one of Pending, Running, Paused, Resuming, Succeeded, Failed or Unknown.

* **conditions** (*[]JobCondition*)

    Represents the latest available observations of a MPIJob's current state.

    *JobCondition* is an observation of the condition of the MPIJob.

    * **type** (*string*)

        Type of Job condition.

    * **status** (*string*)

        Status of the condition, one of True, False, or Unknown.

    * **reason** (*string*)

        The reason for the condition's last transition.

    * **message** (*string*)

        A readable message indicating details about the transition.

    * **lastTransitionTime** (*Time*)

        Last time the condition transitioned from one status to another.

* **aggregate**(*Aggregate*)

    Count the number of replicas in each phase.

    * **creating** (*int32*)

        The number of replicas that is just creating.

    * **pending** (*int32*)

        The number of pending replicas.

    * **running** (*int32*)

        The number of running replicas.

    * **succeeded** (*int32*)

        The number of succeeded replicas.

    * **failed** (*int32*)

        The number of failed replicas.

    * **unknown** (*int32*)

        The number of replicas whose phase is unknwon.

    * **deleted** (*int32*)

        The number of deleted replicas.

* **tasks** (*[]TaskStatus*)

    The statuses of individual tasks.

    *TaskStatus* defines the observed state of the task.

    * **replicaType** (*string*)

        Type of the replica.

    * **replicaIndex** (*int32*)

        Index of the replica.

    * **replicas** (*[]ReplicaStatus*)

        Status of the replica pod.

        *ReplicaStatus* defines the observed state of the pod.

        * **name** (*string*)

            Pod Name.

        * **uid** (*string*)

            Pod UID.

        * **phase** (*PodPhase*)

            Pod phase, one of Creating, Pending, Running, Succeeded, Failed, Unknown or Deleted.

        * **containers** (*[]ContainerStatus*)

            Status of the container named "pytorch" in the pod.

            *ContainerStatus* defines the observed state of the container.

            * **containerPhase** (*string*)

                Phase of the container, one of Waiting, Running, Terminated or Unknown.

            * **exitCode** (*int32*)

                Exit code of the container if it is terminated.
