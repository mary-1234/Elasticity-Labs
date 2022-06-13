# Elasticity-Labs
Labs for Monitoring services(Elastic Load Balancers, Amazon Cloud Watch,AutoScaling)
## Labs on Elastic Load Balancers

### Description
<P>Elastic Load Balancing allows the distribution of incoming traffic to your Amazon AWS infrastructure across multiple instances. This represents a great tool in avoiding failures in your applications and web traffic. ELB automatically detects fails in your EC2 instances and redirects traffic to other available instances. During this Lab, you will learn to create and use your first ELB instance to balance the HTTP traffic between two EC2 instances. You will also gain a valuable understanding of the Classic Load Balancer behavior during an instance outage.</p>

## Step 1: Select a load balancer type

<P>Elastic Load Balancing supports different types of load balancers. For this tutorial, we shall create a Classic Load Balancer.</p>

### To create a Classic Load Balancer

<P>     1.Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2.  On the navigation bar, choose a Region for your load balancer. Be sure to select the same Region that you selected for your EC2 instances.

3.  On the navigation pane, under LOAD BALANCING, choose Load Balancers.

4.  Choose Create Load Balancer.

5. For Classic Load Balancer, choose Create.
  
  ## Step 2: Define your load balancer
  
  <P>You must provide a basic configuration for your load balancer, such as a name, a network, and a listener.

A listener is a process that checks for connection requests. It is configured with a protocol and a port for front-end (client to load balancer) connections and a protocol and a port for back-end (load balancer to instance) connections. In this tutorial, you configure a listener that accepts HTTP requests on port 80 and sends them to your instances on port 80 using HTTP.
  
    To define your load balancer and listener
1.  For Load Balancer name, type a name for your load balancer.

    The name of your Classic Load Balancer must be unique within your set of Classic Load Balancers for the region, can have a maximum of     32 characters, can contain only alphanumeric characters and hyphens, and must not begin or end with a hyphen.

2.  For Create LB inside, select the same network that you selected for your instances: EC2-Classic or a specific VPC.

3.  [Default VPC] If you selected a default VPC and would like to choose the subnets for your load balancer, select Enable advanced VPC configuration.

4.  Leave the default listener configuration.
    
5.  [EC2-VPC] For Available subnets, select at least one available public subnet using its add icon. The subnet is moved under Selected      subnets. To improve the availability of your load balancer, select more than one public subnet.
    
    You can add at most one subnet per Availability Zone. If you select a subnet from an Availability Zone where there is already an selected subnet, this subnet replaces the currently selected subnet for the Availability Zone.

6. Choose Next: Assign Security Groups.

## Step 3: Assign security groups to your load balancer in a VPC
    
<p>To assign security group to your load balancer

1. On the Assign Security Groups page, select Create a new security group.

2. Type a name and description for your security group, or leave the default name and description. This new security group contains a rule that allows traffic to the port that you configured your load balancer to use.
  
3. Choose Next: Configure Security Settings.

4. For this tutorial, you are not using a secure listener. Choose Next: Configure Health Check to continue to the next step.
  
## Step 4: Configure health checks for your EC2 instances
  
<p> Elastic Load Balancing automatically checks the health of the EC2 instances for your load balancer. If Elastic Load Balancing finds an unhealthy instance, it stops sending traffic to the instance and reroutes traffic to healthy instances. In this step, you customize the health checks for your load balancer.
  
 To configure health checks for your instances

1. On the Configure Health Check page, leave Ping Protocol set to HTTP and Ping Port set to 80.

2. For Ping Path, replace the default value with a single forward slash ("/"). This tells Elastic Load Balancing to send health check queries to the default home page for your web server, such as index.html.

3. For Advanced Details, leave the default values.

4. Choose Next: Add EC2 Instances.
  
## Step 5: Register EC2 instances with your load balancer  
  
<p> Your load balancer distributes traffic between the instances that are registered to it.

To register EC2 instances with your load balancer

1. On the Add EC2 Instances page, select the instances to register with your load balancer.

2. Leave cross-zone load balancing and connection draining enabled.

3. Choose Next: Add Tags.

Alternatively, you can register instances with your load balancer later on using the following options:

   .Select running instances after you create the load balancer. For more information,
  see Register Instances with Your Load Balancer.

   .Set up Auto Scaling to register the instances automatically when it launches them.
  For more information,see Set up a scaled and load-balanced application in the Amazon EC2 Auto Scaling User Guide.  
  
## Step 6: Create and verify your load balancer  
  
<P> Before you create the load balancer,review the settings that you selected.
  After creating the load balancer,you can verify that it's sending traffic to your EC2 instances. 
  
  To create and test your load balancer

1. On the Review page, choose Create.

2. After you are notified that your load balancer was created, choose Close.

3. Select your new load balancer.

4. On the Description tab,check the Status row.If it indicates that some of your instances are not in service, its probably because they are still in the registration process.
  
5. After at least one of your EC2 instances is in service, you can test your load balancer. Copy the string from DNS name (for example, my-load-balancer-1234567890.us-west-2.elb.amazonaws.com) and paste it into the address field of an internet-connected web browser. If your load balancer is working, you see the default page of your server.
  
## Step 7: Delete your load balancer
  
<P> To delete your load balancer

1. If you have a CNAME record for your domain that points to your load balancer, point it to a new location and wait for the DNS change to take effect before deleting your load balancer.

2. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

3. On the navigation pane, under LOAD BALANCING, choose Load Balancers.

4. Select the load balancer.

5. Choose Actions, Delete.  
  
6. After you delete a load balancer, the EC2 instances associated with the load balancer should also be terminated as well. 

  
  
  ## B. Labs on Amazon CloudWatch
  
  <P> In this lab,you will Create alarms that stop, terminate, reboot, or recover an instance
     So you can create a CloudWatch alarm that monitors CloudWatch metrics for one of your instances. CloudWatch will automatically send you a notification when the metric reaches a threshold you specify. You can create a CloudWatch alarm using the Amazon EC2 console, or using the more advanced options provided by the CloudWatch console.
    
    To create an alarm using the Amazon EC2 console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. In the navigation pane, choose Instances.

3. Select the instance and choose Actions, Monitor and troubleshoot, Manage CloudWatch alarms.

4. On the Manage CloudWatch alarms detail page, under Add or edit alarm, select Create an alarm.

5. For Alarm notification, choose whether to turn the toggle on or off to configure Amazon Simple Notification Service (Amazon SNS) notifications. Enter an existing Amazon SNS topic or enter a name to create a new topic.

6. For Alarm action, choose whether to turn the toggle on or off to specify an action to take when the alarm is triggered. Select an action from the dropdown.

7. For Alarm thresholds, select the metric and criteria for the alarm. For example, you can leave the default settings for Group samples by (Average) and Type of data to sample (CPU utilization). For Alarm when, choose >= and enter 0.80. For Consecutive period, enter 1. For Period, select 5 minutes.

8. (Optional) For Sample metric data, choose Add to dashboard.

9. Choose Create.
    
    
    ## C. Labs on Amazon Autoscaling Groups
    
<P>    Description
Auto Scaling helps you maintain application availability and allows you to scale your Amazon EC2 capacity up or down automatically according to the defined conditions. You can use Auto Scaling to help ensure that you are running your desired number of Amazon EC2 instances. Auto Scaling can also automatically increase the number of Amazon EC2 instances during demand spikes to maintain performance and decrease capacity during lulls to reduce costs. Auto Scaling is well suited to applications that have stable demand patterns, or that experience hourly, daily, or weekly variability in usage.

    
 ### Step 1: Create a launch template
  
  <P> Choose a region that best suits your business needs
    
1.  Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. On the navigation pane, under Instances, choose Instances.

2. Select the instance and choose Actions, Image and templates, Create template from instance.

3. Provide a name and description.

4. Under Auto Scaling guidance, select the check box.

5. Adjust any settings as required, and choose Create launch template.
    

### Step 2: Create an Auto Scaling Group using a Launch template 
    
<p> 1. Open the Amazon EC2 Auto Scaling console at https://console.aws.amazon.com/ec2autoscaling/.

2. On the navigation bar at the top of the screen, choose the same AWS Region that you used when you created the launch template.

3. Choose Create an Auto Scaling group.

4. On the Choose launch template or configuration page, do the following:

      a. For Auto Scaling group name, enter a name for your Auto Scaling group.

      b. For Launch template, choose an existing launch template.

      c. For Launch template version, choose whether the Auto Scaling group uses the default, the latest, or a specific version of the launch template when scaling out.

      d. Verify that your launch template supports all of the options that you are planning to use, and then choose Next.

5. On the Choose instance launch options page, under Network, for VPC, choose a VPC. The Auto Scaling group must be created in the same VPC as the security group you specified in your launch template.

6. For Availability Zones and subnets, choose one or more subnets in the specified VPC. Use subnets in multiple Availability Zones for high availability. For more information, see Considerations when choosing VPC subnets.
  
7. If you created a launch template with an instance type specified, then you can continue to the next step to create an Auto Scaling group that uses the instance type in the launch template.

Alternatively, you can choose the Override launch template option if no instance type is specified in your launch template or if you want to use multiple instance types for auto scaling. For more information, see Auto Scaling groups with multiple instance types and purchase options.

8. Choose Next to continue to the next step.

Or, you can accept the rest of the defaults, and choose Skip to review.
  
9. On the Review page, choose Create Auto Scaling group.


 
    
    
  
  
