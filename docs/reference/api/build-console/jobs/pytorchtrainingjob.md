# PyTorchTrainingJob

## PyTorchTrainingJob

PyTorchTrainingJob enables running distributed machine learning training tasks in Kubernetes using PyTorch.

* **apiVersion**: batch.tensorstack.dev/v1beta1
* **kind**: PyTorchTrainingJob
* **metadata** ([*ObjectMeta*](https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/object-meta/#ObjectMeta))

  	Standard object's metadata. More info: [https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata](https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata)

* **spec** ([*PyTorchTrainingJobSpec*](#pytorchtrainingjobspec))

  	Specification of the desired behavior of the PyTorchTrainingJob
  
* **status** ([*PyTorchTrainingJobStatus*](#pytorchtrainingjobstatus))

  	Most recently observed status of the PyTorchTrainingJob

## PyTorchTrainingJobSpec

PyTorchTrainingJobSpec is the specification of the desired behavior of the PyTorchTrainingJob.

* **replicaSpecs** (*[]ReplicaSpec*), required

    Describes the spec of the replicas that the job consists of.

    *ReplicaSpec* describes the spec of a replica.

    * **type** (*string*), required

        The type of the replica, one of "master" or "worker".

    * **replicas** (*int32*)

        The desired number of replicas created from the given template. If unspecified, defaults to 1.

    * **template** (*[PodTemplateSpec](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-template-v1/#PodTemplateSpec)*)

        Describes the pod that will be created for this replica. Note that **restartPolicy** in *PodTemplateSpec* will be overidden by **restartPolicy** in *ReplicaSpec*.

    * **restartPolicy** (*string*)

        The restart policy for this replica, one of Always, OnFailure, Never, or ExitCode. Defaults to Never.

    * **scalingWeight** (*int*)
        
        When the elastic training mode is enabled, the controller will allocate the number of replicas for each type based on the scalingWeight.

* **tensorboardSpec** (*[TensorBoardSpec](../tensorboard.md#tensorboardspec)*)

    Describes the Tensorboard to be created for showing training logs.

* **runMode** (*RunMode*)

    PyTorchTrainingJob can run in three modes: normal, debug and pause. Normal - run the job; debug - create training environment but not train; pause - keep the PyTorchTrainingJob CR but not create the workload.

    *RunMode* tells which mode to use and how the job works in this mode.

    * **debug** (*DebugMode*)
   
        *DebugMode* describes how the debug mode works.

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

                Command to execute in the replica, default 'sleep inf'.

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

* **runPolicy** (*RunPolicy*)

    Specifies various rules for managing the running of a PyTorchTrainingJob.

    *RunPolicy* encapsulates various runtime policies of the distributed training job, for example how to clean up resources and how long the job can stay active.

    * **activeDeadlineSeconds** (*int64*)

        Specifies the duration in seconds relative to the startTime that the job may be active before the system tries to terminate it; value must be positive integer.

    * **backoffLimit** (*int32*)

        Optional number of retries before marking this job failed.

    * **cleanUpPolicy** (*string*)

        Clean the tasks after the training job finished, one of "All", "Unfinished" or "None".

* **scheduler** (*SchedulerPolicy*)

    Choose the appropriate Scheduler to schedule replicas. Can be K8s Default Scheduler and T9k Scheduler. Default use K8s Defaule Scheduler.

    *SchedulerPolicy* assign the replicas to a specific scheduler.

    * **t9kScheduler** (*T9kScheduler*)

        T9k Scheduler configuration.

        *T9kScheduler* descibes the PodGroup that will be created.

        * **Queue** (*string*), required

            T9k Scheduler Queue name. All T9k Scheduler PodGroups should work in a Queue.
        
        * **priority** (*int32*)

            Indicates the PodGroup's priority. range is [0,100]. Default 10.

* **elastic** (*ElasticConfig*)

    Adjust job scale dynamically.

    *ElasticConfig* describe the elastic config of PyTorchTrainingJob.

    * **enable** (*bool*)

        Whether to eable elastic mode.

    * **minReplicas** (*int*)

        The minimum number of running nodes in elastic mode.

    * **maxReplicas** (*int*)

        The maximum number of running nodes in elastic mode.

    * **expectedReplicas** (*int*)

        The expected number of running nodes in elastic mode.

* **torchrunConfig** (*TorchrunConfig*)
    
    PyTorch provides a tool - torchrun(torch.distributed.run) - to launcher pytorch training. Set this config to use torchrun to launch pytorch training.

    *TorchrunConfig* set torchrun args.

    * **enable** (*bool*)

        Whether to use torchrun to launcher pytorch training or not.

    * **maxRestarts** (*int*)
    
    * **procPerNode** (*string*)

        Processes num executed on every replica.
    
    * **rdzvBackend** (*string*)
    
    * **extraOptions** (*[]string*)

## PyTorchTrainingJobStatus

PyTorchTrainingJobStatus is the most recently observed status of the PyTorchTrainingJob.

* **tasks** (*[]TaskStatus*)

    The statuses of individual tasks.

    *TaskStatus* defines the observed state of the task.

    * **type** (*string*)

        Type of the replica.

    * **restartCount** (*int16*)

        The times the pod restart.

    * **replicaStatus** (*[]ReplicaStatus*)
      
        Status of relica.
      
        *ReplicaStatus* Describe observed state of the replica.

        * **name** (*string*)

          	Sub-resource's name used to distinguish sub-resources. It isn't K8s resource name.

        * **uid** (*string*)

          	UID of replica.

        * **phase** (*string*)

          	Phase of the pod, one of Pending, Running, Succeeded, Failed or Unknown.

        * **containers** (*[]ContainerStatus*)

            Status of the containers in the pod.

            *ContainerStatus* defines the observed state of the container.

            * **name** (*string*)
    
              	Sub-resource's name used to distinguish sub-resources. It isn't K8s resource name.
    
            * **state** (*string*)
    
              	State of container.
    
            * **exitCode** (*int32*)
    
            	Exit code of the container if it is terminated.

* **tensorboard** (*DependentStatus*)

    The status of the tensorboard if there is one.

    *DependentStatus* is the status of a K8s dependent object.

    * **name** (*string*)

      	Sub-resource's name used to distinguish sub-resources. It isn't K8s resource name.

    * **dependent** (*[ObjectReference](https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/object-reference/)*)

      	Refers to a K8s resource.

    * **ready** (*bool*)

      	Whether the sub-resource is ready to work.

    * **reason** (*string*)

      	The reason why the sub-resource is in this status.

    * **action** (*string*)

      	An action for reconciling a dependent.

    * **note** (*string*)

      	A note that gives more information about this status.

    * **type** (*string*)

      	Status type, one of Normal or Warning.

* **backoffCount** (*int32*)

  	The number of restarts being performed.

* **aggregate** (*Aggregate*)
  
  	The number of tasks in each state.

  	*Aggregate* count the number of tasks in each state.

    * **creating** (*int32*)

      	The number of tasks in unknown state (Pod is not available).

  	* **pending** (*int32*)

    	The number of tasks in pending state (Pod is in waiting state).

  	* **running** (*int32*)

    	The number of tasks in running state (Pod is in running state).

  	* **succeeded** (*int32*)

    	The number of tasks in succeeded state (Pod is terminated with exit code =  0).

    * **failed** (*int32*)

  		The number of tasks in failed state (Pod is terminated with exit code != 0).

    * **unknown** (*int32*)

		The number of tasks in unknown state (Pod is not available).

	* **deleted** (*int32*)

		The number of tasks in deleted state (Pod is deleted).

* **conditions** (*[]JobCondition*)

  	Represents the latest available observations of a PyTorchTrainingJob's current state.

  	*JobCondition* is an observation of the condition of the PyTorchTrainingJob.

    * **type** (*string*)

      	Type of Job condition.

    * **status** (*string*)

      	Status of the condition, one of True, False, or Unknown.

    * **reason** (*string*)

      	The reason for the condition's last transition.

    * **message** (*string*)

      	A readable message indicating details about the transition.

    * **lastTransitionTime** (*string*)

      	Last time the condition transitioned from one status to another.

* **phase** (*string*)

  	Defines all possible phases of training, one of Pending, Running, Paused, Resuming, Succeeded, Failed or Unknown.
