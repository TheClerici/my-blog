---
layout: post
title:  "Learning week b4 client"
date:   2023-03-19 10:00:25 -0000
category: Weekly
---
## Welcome to my weekly post!

Hello guys!! Happy to announce that I'm gonna start with a client on the next days to come, currently waiting on my credentials so I can get everything started, I'm really excited about this new chapter in my life, so come follow me on the new learnings I got in preparation to start with them.

I decided to focus mainly on AWS and message queues, and also added a little bit to my git knowledge with stashing.

* What is Stashing?

Stashing is a feature of version control systems like Git that allows developers to save their changes without committing them to the repository. When you stash your changes, Git stores them in a special area called the stash. This area acts like a temporary storage location for your changes until you're ready to commit them.

* How Does Stashing Work?

When you stash your changes, Git takes a snapshot of your current working directory and saves it in the stash. This snapshot includes all the changes you've made since your last commit. Git also reverts your working directory to the state of the last commit, effectively erasing your changes from the directory.

Once you've stashed your changes, you can switch to another branch or task without worrying about losing your work. When you're ready to resume working on your original branch or task, you can simply apply the stash to your working directory. Git will then merge your changes with the changes that have been made since you stashed your work.

Queuing technologies are essential components of modern distributed systems. They allow applications to send and receive messages asynchronously, providing a way to decouple components and improve system reliability. RabbitMQ is a popular message broker that provides a robust and scalable queuing solution. In this blog post, we'll continue with RabbitMQ and its use cases in distributed systems.

* How Does RabbitMQ Work?

RabbitMQ is based on a producer-consumer model, where producers send messages to queues and consumers receive messages from queues. The messages are sent using the AMQP protocol, which provides a standardized way to encode and transmit messages. RabbitMQ also supports other messaging protocols such as STOMP, MQTT, and HTTP.

In RabbitMQ, messages are stored in queues until they are consumed by consumers. Each queue has a name and is identified by a routing key, which specifies the message type or content. Consumers can subscribe to one or more queues and receive messages as they arrive. RabbitMQ provides several strategies for message distribution, including round-robin, priority-based, and topic-based routing.

RabbitMQ also supports several features that improve system reliability, including message acknowledgment, message durability, and message expiration. Message acknowledgment ensures that a message is not lost if a consumer crashes or fails to process the message. Message durability ensures that messages are not lost if RabbitMQ crashes or restarts. Message expiration ensures that messages are automatically removed from queues after a specified time period.

Cloud computing has become an essential technology for modern businesses and individuals, providing a flexible, scalable, and cost-effective way to access computing resources and services. Cloud computing allows users to access applications, data storage, and computing power over the internet, without the need for expensive hardware and infrastructure. Cloud computing also enables users to scale resources up or down as needed, allowing them to quickly adapt to changing business needs. Additionally, cloud computing provides improved security and reliability, with data backups, disaster recovery, and access controls built into the platform.

AWS is inmence, And on this blog I will talk about the first two components I have looked into, which are AWS Identity and Access Management (IAM) and Virtual Private Cloud (VPC), we'll explore IAM and VPC and their importance in securing and managing AWS resources.

* AWS Identity and Access Management (IAM)

IAM is a web service that allows you to manage access to AWS resources securely. With IAM, you can create and manage users, groups, and roles, and assign permissions to them to access AWS resources. IAM provides fine-grained access control, allowing you to grant permissions to specific actions on specific resources.

IAM provides several features that improve security and compliance, including multi-factor authentication (MFA), password policies, and access logging. MFA adds an extra layer of security by requiring users to provide a second form of authentication, such as a code from a mobile app or a hardware token. Password policies enforce strong password requirements, such as minimum length and complexity, to prevent unauthorized access. Access logging allows you to monitor and audit user activity in your AWS account, providing visibility into who accessed what resources and when.

IAM is essential for managing access to AWS resources, especially in large organizations with multiple users and teams. With IAM, you can ensure that users have the appropriate level of access to AWS resources, and you can easily revoke access when needed. IAM also integrates with other AWS services, such as Amazon S3 and AWS Lambda, allowing you to grant permissions to specific actions on these services.

* Virtual Private Cloud (VPC)

VPC is a service that allows you to create a private network in the AWS cloud. With VPC, you can create subnets, configure routing, and control network access. VPC provides several benefits, including improved security, isolation, and scalability.

VPC allows you to create a private network that is isolated from the public internet, providing an extra layer of security. You can configure security groups and network access control lists (ACLs) to control access to resources within your VPC. You can also create VPN connections between your on-premises network and your VPC, allowing you to extend your network into the cloud.

VPC also allows you to create multiple subnets within your VPC, providing granular control over network routing and resource placement. You can configure routing tables to control traffic between subnets and to the internet. You can also create private subnets that do not have a direct route to the internet, providing additional isolation and security.

VPC is essential for deploying applications in the AWS cloud, especially in scenarios where security and isolation are critical. With VPC, you can create a private network that is customized to your specific requirements, and you can easily scale your network as your needs evolve.

We have explored several important topics in the field of technology, ranging from software development methodologies and version control systems to queuing technologies and cloud computing. We have discussed the benefits and challenges of different software development methodologies, such as Agile and Waterfall, and explored how version control systems like Git and GitHub can help developers manage code changes and collaborate effectively.

We have also delved into queuing technologies, specifically RabbitMQ, and how they can help manage messaging and task processing in distributed systems. Finally, we explored two fundamental components of Amazon Web Services (AWS), Identity and Access Management (IAM), and Virtual Private Cloud (VPC), and their importance in securing and managing AWS resources.

Overall, these topics represent a diverse set of technological advancements and concepts that are critical in today's rapidly evolving digital landscape. 