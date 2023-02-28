---
title: What's a Job/Batch/Pipeline
metaTitle: What's a Job/Batch/Pipeline
metaDescription: A quick guide on the GNJ models.
sidebar: Documentation
hideAnchor: false
showTitle: true
---

A quick guide on the GNJ models.
![Alt text](/assets/models-schema.png)
_A representation of the most complex use case in GNJ._

---

Quick sum-up :

- Jobs are **dispatched** sequentially but can be **run in parallel**.
- Jobs inside a Pipeline are **dispatched** AND **executed** sequentially.
- Jobs inside a Pipeline linked to a batch are **dispatched** sequentially but **run in parallel**.

---

## The job

Jobs are the most important part of GNJ. They represent the execution of a type of task.

Your workers can query GNJ to fetch jobs of one or more type to be executed.

They are DISPATCHED **sequentially**. When a worker is asking for something to perform, they are returned in a **FIFO** way.

Yet, they are only "dispatched" sequentially, not executed. So if you have two workers processing jobs at the same time. The worker 1 (W1) will receive the Job 1 (J1) before the worker 2 (W2) will receive the job 2 (J2). But if W2 executes the job faster that W1, J1 will be done before J2 is done.

If you need to execute J2 **after** J1 is done and not before, you can simply insert J2 in the queue at the end of J1. It's the recommended way.

Another alternative, is to assign only one worker to a type of job. Then you can make sure that J2 will be only executed after J1 if they share the same type.

The last option, that we do not recommend if the two lasts options are not possible, is to create a pipeline.

---

## The pipeline

When jobs must be created in advance, for exemple if they must be reviewed/validated by an humain before being started, and when you want to **execute** them **sequentially**, you must create a pipeline.

A pipeline will ensure that:

- Jobs inside the pipeline must be executed sequentially
- The jobs are still provided as a FIFO list, so create them accordingly
  - A way to sort jobs is currently is study.
- If a job of the pipeline fails, the following jobs will never be executed

---

## The batch

If you are using a pipeline, and a set of your jobs must be run in parallel, you will need to use the batches.

A batch is a series of job, inside a pipeline, that will not be run sequentially.

- If any job of a batch fail, the batch is considered "failed"
- The pipeline of a failed batch will be considered as "failed"
- Job will stop being dispatched inside a pipeline as soon as it is "failed"

Be careful, if you have only one worker in charge of the batch's jobs, it will have no effect and they will still run sequentially.
