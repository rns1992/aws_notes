# Step Functions

### What is Step Functions?
- It provides a visual interface for serverless applications, which enables us to build and run serverless applications as a series of steps. 
- Each step in our application executes in order, as defined by our business logic.
- The output of one step may act as an input to the next.
- Step functions also log the state of each step, so when things do go wrong, you can diagnose and debug problems quickly because we would be able to identify which step in the process failed.

### What is State Machine and Tasks in Step Function?
- State Machine is simply the workflow itself and Task is single step or single unit of work that makes up the work flow.

### How many types of workflows we have in step function?
- We can have 3 different workflows
	1) Sequential Workflow - Operates sequentially
	2) Parallel Workflow - Operates parallelly
	3) Branching Workflow - Operates based on condition if true the this task or else this task.

### Exam Tips
1) **Visualize**
	- Its a great way to visualize your serverless applciation.
2) **Automate**
	- Step Function automatically trigger and track each step. The output of one step is often the input to the next step.
3) **Logging**
	- Step Functions log the state of each step, so if something goes wrong we can track what went wrong and where.


### What is Standard Workflows?
1) **Long Running**
	 - It is a **long running**, **durable** and **auditable** workflows that may run **up to a year**.
	 - Its full execution history is available for up to 90 days after its completion.
2) **At-Most-Once-Model**
	- Tasks are **never** executed **more than once** unless you explicitly specify retry actions.
3) **Non-Idempotent Actions**
	- When processing payments, we only want a payment to be processed once, not multiple times.
4) **Non-Idempotent**
	- A request is non idempotent if it always causes a change in state (e.g. sending the same email multiple times causes a change in state because you end up with multiple emails in your inbox)

### What are Express Workflows?
1) **Short Lived**
	- Great for high-volume, event processing-type workloads
	- It normally is a small process which is for example for 5 mins.
2) **At-Least-Once**
	- Ideal if there is a possibility that an execution might be run more than once or we require multiple concurrent executions.
3) **Idempotent**
	- For example, transforming input data and storing the result in DynamoDB.
4) **Identical Request**
	- A request is considered idempotent if an identical request can be made once or several times in a row with no additional side effects (e.g. reading data from a database or S3 bucket).
	- It has no side effects

### How many types of Express Workflows are there?
1) **Synchronous Express Workflow**
	- *Step 1*: It begins the workflow.
	- *Step 2*: Waits until it completes.
	- *Step 3*: Returns the result.
	- *Step 4*: Continues for next task.
	- It is suitable for operations that are performed one at a time. The workflow must complete before the next step begins.
2) **Asynchronous Workflow**
	- *Step 1*: It begins the workflow.
	- *Step 2*: Confirms the workflow has started.
	- *Step 3*: The result of the workflow can be found in CloudWatch Logs.
	- *Step 4*: Great if services or operations don't depend on the completion and result of your workflow.
