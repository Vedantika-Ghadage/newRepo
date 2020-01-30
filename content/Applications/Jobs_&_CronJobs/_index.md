+++
title = "Jobs & CronJobs"
description = ""
weight=100
+++
{{%excerpt%}}

Jobs are actions created and added to an application to run once.

Most commonly, Jobs are used to cleanup after an application runs, to run security before deploying an application, or to perform one-time setup operations.

It is possible to add multiple jobs to a single application.

CronJobs in Nirmata are equivalent to CronJobs in Linux. Using CronJobs, users can schedule jobs to be performed at predetermined intervals. CronJobs are most commonly used to create current snapshots and to backup snapshots.

#### How to Create a Job in an Application

To add a Job to an application, open the application and select *Add a Job*.

![image](/images/jobs-1.png)

Complete each tab of the *Add a Job* wizard.

![image](/images/jobs-2.png)

![image](/images/jobs-3.png)

![image](/images/jobs-4.png)

#### How to Create a CronJob in an Application

To add a CronJob to an application, open the application and select *Add a CronJob*.

![image](/images/jobs-5.png)

Complete each tab of the *Add a CronJob* wizard.

![image](/images/jobs-6.png)

![image](/images/jobs-7.png)

![image](/images/jobs-8.png)

{{%/excerpt%}}
