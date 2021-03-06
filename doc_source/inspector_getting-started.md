# Getting Started with Amazon Inspector<a name="inspector_getting-started"></a>

Set up Amazon Inspector and get started by creating and running your first assessment\.

**Important**  
To use Amazon Inspector you must have an Amazon Web Services \(AWS\) account\. When you sign up for AWS, your account is automatically signed up for all services in AWS, including Amazon Inspector\. If you don't have an AWS account, use the following procedure to create one\.  
Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.  
If you previously signed in to the AWS Management Console using AWS account root user credentials, choose **Sign in to a different account**\. If you previously signed in to the console using IAM credentials, choose **Sign\-in using root account credentials**\. Then choose **Create a new AWS account**\.
Follow the online instructions\.  
Part of the sign\-up procedure involves receiving a phone call and entering a verification code using the phone keypad\.

**Topics**
+ [Pre\-Requisites for Using Amazon Inspector](#pre-requisites)
+ [One\-Click Setup](#inspector_basic-assessment)
+ [Advanced Setup](#inspector_custom-assessment)

## Pre\-Requisites for Using Amazon Inspector<a name="pre-requisites"></a>

When you launch the Amazon Inspector console for the first time, choose **Get Started** and complete the following prerequisite tasks\. You must complete these tasks before you can perform an Amazon Inspector assessment run:
+ You must have at least one Amazon EC2 instance running in your AWS environment in order to run an Amazon Inspector assessment\. For more information about launching EC2 instances, see [ Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/)\.
+ In most cases, the Amazon Inspector Agent must be running on each EC2 instance in your assessment target\. For more information about installing Amazon Inspector agents, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)\. Alternatively, you can choose an option while setting up an assessment to install the agent on your Amazon EC2 instances if those instances allow the [Systems Manager Run Command](https://docs.aws.amazon.com/systems-manager/latest/userguide/execute-remote-commands.html)\. For more information about Amazon Inspector Agents, see [Amazon Inspector Agents](inspector_agents.md)\. 

## One\-Click Setup<a name="inspector_basic-assessment"></a>

The following procedure shows you how to create and run an automatic assessment using a pre\-built template and pre\-defined scheduling parameters \(once a week or one\-time\) on all available EC2 instances in the current AWS account and region\. 

1. On the **Welcome** page, choose the type of assessment you would like to perform\. **Network Assessments** analyze the network configurations of your AWS environment for vulnerabilities, and do not require the presence of an Amazon Inspector Agent\. **Host Assessments** analyze the on\-host software and configurations of your EC2 instances for vulnerabilities, and requires the Inspector agent to be installed on the EC2 instances\.

   Choose either **Run weekly \(recommended\)** or **Run once**\. As soon as you make your choice, the service automatically creates the assessment for you\. Specifically, the service does the following: 

   1. Creates a [service\-linked role](inspector_slr.md)\.
**Note**  
Amazon Inspector needs to enumerate your EC2 instances and tags to identify the EC2 instances specified in the assessment targets\. Amazon Inspector gets access to these resources in your AWS account through a service\-linked role called `AWSServiceRoleForAmazonInspector`\. For more information about service\-linked roles, see [Using Service\-Linked Roles for Amazon Inspector](inspector_slr.md) and [Using Service\-Linked Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\. 

   1. If applicable, installs an [Amazon Inspector agent](inspector_agents.md) on all available Amazon EC2 instances in your AWS account and AWS region\. 
**Note**  
The service installs an Amazon Inspector agent only on those EC2 instances that allow System Manager Run Command\. To use this option, make sure that all of your EC2 instances in the current AWS account and AWS region have the SSM Agent installed and has an IAM role that allows Run Command\. For more information, see [To install the Amazon Inspector Agent on multiple EC2 instances using the Systems Manager Run Command](inspector_installing-uninstalling-agents.md#install-run-command)\.

   1. Adds those instances to an [assessment target](inspector_applications.md)\.

   1. Includes that target in an [assessment template](inspector_assessments.md) with a standardized set of rules packages\.

   1. Runs the assessment weekly or only once, depending on whether you chose **Run weekly \(recommended\)** or **Run once**\.

1. In the **Confirmation** dialog box, choose **OK**\. Amazon Inspector automatically runs your assessment\. 

## Advanced Setup<a name="inspector_custom-assessment"></a>

The following procedure shows you how to complete the advanced Amazon Inspector setup guide to choose specific Amazon EC2 instances, rules packages, and scheduling parameters to include in an assessment target and template\.

1. On the **Welcome** page, choose **Advanced setup**\.

1. On the **Define an assessment target** page, enter the name of your assessment target\. 

1. For **All Instances**, you can keep the check box selected to include all EC2 instances in your AWS account and Region in the assessment target\. If you want to choose which EC2 instances to include, clear the **All Instances** check box, and enter the **Key** and **Value** tags associated with the target EC2 instances\. For more information about tagging your EC2 instances, see [ Tagging Your Amazon EC2 Resources](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html)\.

1. For **Install Agents**, you can keep the check box selected by default if your instances allows [System Manager Run Command](https://docs.aws.amazon.com/systems-manager/latest/userguide/execute-remote-commands.html                         )\. The service installs an Amazon Inspector agent on all EC2 instances in the assessment target that allow System Manager Run Command\. To use this option, make sure that all of your EC2 instances in the current AWS account and AWS region have the SSM Agent installed and has an IAM role that allows Run Command\. For more information, see [To install the Amazon Inspector Agent on multiple EC2 instances using the Systems Manager Run Command](inspector_installing-uninstalling-agents.md#install-run-command)\. If you want to manually install the agent, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)\.

1. Choose **Next**\.

1. On the **Define an assessment template** page, enter the name of your assessment template\.

1. For **Rules packages**, choose the rules packages to include in the assessment template\. For more information about rules packages, see [Amazon Inspector Rules Packages and Rules](inspector_rule-packages.md)\.

1. For **Duration**, choose the duration of your assessment run\.

1. For **Assessment Schedule**, you can set a schedule for recurring assessment runs\.

1. Choose **Next**\.

1. On the **Review** page, review your choices for the assessment target and template\. If you are satisfied with the configuration, choose **Create**\. If you set an assessment schedule for your assessment template, the assessment will automatically run upon creation\.
**Note**  
Amazon Inspector needs to enumerate your EC2 instances and tags to identify the EC2 instances specified in the assessment targets\. Amazon Inspector gets access to these resources in your AWS account through a service\-linked role called `AWSServiceRoleForAmazonInspector`\. For more information about service\-linked roles, see [Using Service\-Linked Roles for Amazon Inspector](inspector_slr.md) and [Using Service\-Linked Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\. 

1. If you did not set up an assessment schedule, navigate to your assessment template through the console and choose **Run**\.

1. To track the progress of the assessment run, in the navigation pane of the console, choose **Assessment runs**, and then choose **Findings**\. For more information about findings, see [Amazon Inspector Findings](inspector_findings.md)\.