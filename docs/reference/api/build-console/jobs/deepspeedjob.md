# DeepSpeedJob

## DeepSpeedJob

DeepSpeedJob enables running distributed machine learning training tasks in Kubernetes using DeepSpeed.

* **apiVersion**: batch.tensorstack.dev/v1beta1
* **kind**: DeepSpeedJob
* **metadata** ([*ObjectMeta*](https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/object-meta/#ObjectMeta))

  	Standard object's metadata. More info: [https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata](https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata)

* **spec** ([*DeepSpeedJobSpec*](#deepspeedjobspec))

  	Specification of the desired behavior of the DeepSpeedJob
  
* **status** ([*DeepSpeedJobStatus*](#deepspeedjobstatus))

  	Most recently observed status of the DeepSpeedJob

## DeepSpeedJobSpec

DeepSpeedJobSpec is the specification of the desired behavior of the DeepSpeedJob.

* **elastic** (*ElasticConfig*)

    Describe how the DeepSpeedJob will run in elastic mode.

    *ElasticConfig* describe the elastic config of DeepSpeedJob.

    * **enable** (*bool*)

        Whether to eable elastic mode in deepspeed.

    * **minReplicas** (*int*)

        The minimum number of running nodes in elastic mode.

    * **maxReplicas** (*int*)

        The maximum number of running nodes in elastic mode.

    * **expectedReplicas** (*int*)

        The expected number of running nodes in elastic mode.


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

* **worker** (*Worker*), required

    Describe the spec of the worker

    * **replicas** (*int32*)

        The desired number of replicas created from the given template. If unspecified, defaults to 1.

    * **restartPolicy** (*string*)

        The restart policy for this replica, one of Always, OnFailure, Never, or ExitCode. Defaults to Never.

    * **template** (*[PodTemplateSpec](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-template-v1/#PodTemplateSpec)*)

        Describes the pod that will be created for this replica. Note that **restartPolicy** in *PodTemplateSpec* will be overidden by **restartPolicy** in *ReplicaSpec*.

* **config** (*Config*), required

    Describe the DeepSpeed config of DeepSpeedJob

    * **run** (*RunType*)

        Describe how the program will be run by DeepSpeed.

        *RunType* describe the type, file, args of program. Only one type can be specified.

        * **python** (*[]string*)

            Describe python script and its args.
        
        * **Module** (*[]string*)
            
            Describe the python module and its args.

        * **Exec** (*[]string*)

            Describe the executable file and its args.

    * **slotsPerWorker** (*int*)

        The number of slots for each worker. Usually equal to the number of GPUs.

    * **localRank** (*bool*)

        Weather to not pass `--no_local_rank` to the DeepSpeed command, defaults to true.
    
    * **autotune** (*string*)

        The autotuning type for deepspeed, one of "tune", "run".

    * **otherArgs** (*[]string*)
  
        Other args for the deepspeed command.

* **disableCustomEnv** (*bool*)

    Whether to disable custom environment variable.

* **runMode** (*RunMode*)

    DeepSpeedJob can run in three modes: normal, debug and pause. Normal - run the job; debug - create training environment but not train; pause - keep the GenericJob CR but not create the workload.
    
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

* **runPolicy** (*RunPolicy*)

    Specifies various rules for managing the running of a DeepSpeedJob.

    *RunPolicy* encapsulates various runtime policies of the distributed training job, for example how to clean up resources and how long the job can stay active.

    * **activeDeadlineSeconds** (*int64*)

        Specifies the duration in seconds relative to the startTime that the job may be active before the system tries to terminate it; value must be positive integer.

    * **backoffLimit** (*int32*)

        Optional number of retries before marking this job failed.

    * **cleanUpPolicy** (*string*)

        Clean the tasks after the training job finished, one of "All", "Unfinished" or "None".

## DeepSpeedJobStatus

DeepSpeedJobStatus is the most recently observed status of the DeepSpeedJob.

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

  	Represents the latest available observations of a DeepSpeedJob's current state.

  	*JobCondition* is an observation of the condition of the DeepSpeedJob.

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
