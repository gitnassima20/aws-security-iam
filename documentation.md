## Cloud Security with AWS IAM

### 1. Introducing today's project!

**What is AWS IAM?**
AWS IAM manages user access and permissions for AWS resources, helping
control who can access specific services and enforce security policies.

**How I'm using AWS IAM in this project**
In todayʼs project, I used AWS IAM to create and manage policies, define
permissions for EC2 actions, and control access based on resource tags,
ensuring secure and appropriate access for different users.

**One thing I didn't expect...**
One thing I didn't expect in this project was the ability to test policies using the
Policy Simulator. It helps ensure policies work as intended without affecting
functional resources in the AWS environment.

**This project took me...**
This project took me 1 hour and 15 minutes, including documentation.


### 2. Tags:

Tags are like labels you can attach to AWS resources for organization.They are
useful for organizing, identifying, and managing resources, enabling cost
tracking, automation, and filtering.

The tag I've used for my EC2 instances is called **Env** and the value I have
assigned for my instances are **production** and **development** to label the
instances used in production vs development environments.

![alt text](aws-security-iam/screeshots/tags-panel-setup.PNG)

### 3. IAM Policies:

IAM Policies are a set of **permissions** that can be attached to *users*, u*ser
groups*, or *roles*, defining what **actions** they can perform on **AWS resources**.

**The policy I set up**
For this project, Iʼve set up a policy using JSON, as it provides more control and
flexibility for defining specific permissions compared to the visual editor.

Iʼve created a policy that allows full EC2 access for resources tagged Env:
development, permits read-only Describe actions for all EC2 resources, and
denies permissions to create or delete tags on any EC2 resource.

**When creating a JSON policy, you have to define its Effect, Action and Resource.**
The Effect, Action, and Resource attributes of a JSON policy mean: Effect
determines whether to *allow or deny* actions, Action specifies the *AWS operations* 
(e.g., ec2:*), and Resource defines the targeted 
*AWS resources* (e.g., * for all resources).

**My JSON Policy**

![alt text](aws-security-iam/screeshots/policy-json-vis.PNG)

### 4. Account Alias:

An account alias is a **friendly name** for your AWS account, making it easier to
identify and access your account in the AWS Management Console instead of
using the **default AWS account ID**.

Now, my new AWS console sign-in URL is: 'https://spacegalaxy.signin.aws.amazon.com/console'

![alt text](aws-security-iam/screeshots/account-alias.PNG)

### 5. IAM Users and User Groups:

**Users**
IAM users are the **people or apps** that will get **access to your resources/AWS account**.

**User Groups**
An IAM user group is a **collection/folder of IAM users**. It allows you to manage
permissions for all the users in your group at the same time by attaching
policies to the group rather than individual users.

I attached the policy I created to this user group, which means the users in the
group will have full EC2 access for resources tagged with Env: development,
read-only access to all EC2 resources, and will be restricted from creating or
deleting tags.

### 6. Logging in as an IAM User:


The first way is to share the new user their sign-in URL, username, and
temporary password is by copy-pasting it. The second way is to download the .csv file
containing the sign-in details and share it securely with the user.

Once I logged in as my IAM user, I noticed several access denied messages.
This is because the IAM userʼs permissions are restricted by the attached
policies, limiting access to certain resources and actions.

![alt text](aws-security-iam/screeshots/IAM-user-signin-details.PNG)


### 7. Testing IAM Policies:

I tested my JSON IAM policy by attempting to stop the production and the
development EC2 instances.

**Stopping the production instance**
When I tried to stop the production instance, the action was denied. This
occurred because the policy only doesn't allow actions on EC2 instances
tagged with Env: production.

![alt text](aws-security-iam/screeshots/not-authorized-to-stop-instance-err.PNG)


**Stopping the development instance**
Next, when I tried to stop the development instance, the action was successful.
This was because the policy allows full access to EC2 instances tagged with
Env: development.

![alt text](aws-security-iam/screeshots/stopping-dev-instance-success-banner.PNG)

### 8.Policy simulator:

If you're working on a real project, you don’t want to test policies casually by applying them directly to resources. Instead, it’s safer and more efficient to use the Policy Simulator to verify that your policies behave as expected without risking any impact on functional resources.

![alt text](aws-security-iam/screeshots/IAM-Policy-Stimulator.PNG)

Thank you to https://learn.nextwork.org/ for your guidance \(￣︶￣*\))