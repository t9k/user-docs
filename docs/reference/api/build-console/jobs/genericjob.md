---
title: GenericJob
---

# GenericJob

## GenericJob

GenericJob enables running distributed computing tasks in Kubernetes through using multiple replicas.

* **apiVersion**: batch.tensorstack.dev/v1beta1
* **kind**: GenericJob
* **metadata** ([*ObjectMeta*:octicons-link-external-16:](https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/object-meta/#ObjectMeta){target=_blank})

    Standard object's metadata. More info: [https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata:octicons-link-external-16:](https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata){target=_blank}.

* **spec** ([*GenericJobSpec*](#genericjobspec))

    Specification of the desired behavior of the GenericJob.

* **status** ([*GenericJobStatus*](#genericjobstatus))

    Most recently observed status of the GenericJob.

## GenericJobSpec

GenericJobSpec is the specification of the desired behavior of the GenericJob.

* **successRules** (*[]FinishedRule*), required

    Rules used to check if a generic job is succeeded. Each role refers to a series of replicas, and the generic job is succeeded only if all of the replicas are succeeded. 

    *FinishedRule* (*map[string]RankList*) is a map from replica role to a list of replica ranks. 

    *RankList* (*[]intstr.IntOrString*) is a list of replica ranks.

    *intstr.IntOrString* is a type that can hold an int32 or a string. When used in JSON or YAML marshalling and unmarshalling, it produces or consumes the inner type. This allows you to have, for example, a JSON field that can accept a name or number

* **failureRules** (*[]FinishedRule*), required

    Rules used to check if a generic job is failed. Each role refers to a series of replicas, and the generic job is failed only if all of the replicas are failed. 

* **service** (*ServiceOption*)

    Service describes whether the service will be create and what the service is like.     

    * **ports** (*[]corev1.ServicePort*)
    
        The list of ports that are exposed by the service which will be created.

        *ServicePort* contains information on service's port. More info: [https://kubernetes.io/docs/reference/kubernetes-api/service-resources/service-v1/#ServiceSpec:octicons-link-external-16:](https://kubernetes.io/docs/reference/kubernetes-api/service-resources/service-v1/#ServiceSpec){target=_blank}.

* **runMode** (*RunMode*)

    GenericJob can run in three modes: normal, debug and pause. Normal - run the job; debug - create training environment but not train; pause - keep the GenericJob CR but not create the workload.
    
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

* **cleanUpPolicy** (*string*)

    Determine whether the replicas should be deleted after the job is finished. Can be `All`, `Unfinished` or `None`.

* **scheduler**

    Choose the appropriate Scheduler to schedule replicas. Can be Kubernetes Default Scheduler or T9k Scheduler. Default use Kubernetes Default Scheduler.

    *SchedulerPolicy* assign the replicas to a specific scheduler.

    * **t9kScheduler** (*T9kScheduler*)

        T9k Scheduler configuration.

        *T9kScheduler* descibes the PodGroup that will be created.

        * **queue** (*string*), required

            T9k Scheduler Queue name. All T9k Scheduler PodGroups should work in a Queue.

        * **priority** (*int32*)

            Indicates the PodGroup's priority. range is [0,100]. Default 0.

* **replicasSpec** (*[]ReplicaSpec*)

    Specify how the replicas work.

    *ReplicaSpec* defines the desired state of replicas.

    * **type** (*string*)

        Replica type. For example, in tensorflow framework, a replica can be master, worker or ps.

    * **replicas** (*int32*)
    
        The desired number of replicas of the given template.
    
    * **restartPolicy** (*RestartPolicy*)

        The policy to deal with failed replica.

        *RestartPolicy* tells what to do if a replica is failed.

        * **policy** (*string*)

            The policy to handle failed replica. Can be `Always`, `OnFailure` or `Never`.

        * **limit** (*int16*)

            The max time replicas can restart.

    * **template** ([*PodTemplateSpec*:octicons-link-external-16:](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-template-v1/#PodTemplateSpec){target=_blank})

        Template describes the Pods that will be created.

## GenericJobStatus

GenericJobStatus is the most recently observed status of the GenericJob.

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

  	Represents the latest available observations of a GenericJob's current state.

  	*JobCondition* is an observation of the condition of the GenericJob.

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
