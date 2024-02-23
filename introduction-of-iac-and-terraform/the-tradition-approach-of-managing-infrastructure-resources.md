# The tradition approach of managing infrastructure resources

Before we dive into what Infrastructure as Code (IaC) is all about, let's take a quick trip down memory lane to the old days of setting up and managing tech systems. Understanding the struggles we faced back then will make it clear why we're now moving towards new concepts and tools.\


Imagine you are a data scientist in a E-Commerce company, which is very open to new technology and already adopted the cloud services on the Google Cloud platform. You need a new compute instance for your machine learning project, how do you get that virtual machine up and running?\


The first answer jumping out from my mind is the user-friendly graphical user interface (GUI). Everybody can create a virtual machine easily and intuitively just by a few clicks. And when the GUI isn't playing hard to get, some tech-savvy folks might resort to the Command Line – a bit more nerdy, but it gets the job done faster. For example

```
cloud compute instances create VM_NAME \
  --zone=ZONE \
  [--image=IMAGE | --image-family=IMAGE_FAMILY] \
  --image-project=IMAGE_PROJECT 
```

For managing a few resources, these two methods are ideal. However, real-world business requirements are far more complex and varied than such a straightforward scenario.

What if we need to create and manage 20 virtual machines cross 3 regions and 5 departments?

You might say the former ways are not appropriate for this need and you would not create the resources 20 times for different provision requirements. You are completely right.&#x20;

Creating infrastructure manually and one at a time, isn't just slow – it's ripe for mistakes. Typos, wrong settings, and missing instructions are all too easy to make, not because we're careless, but because we're human. Clearly, it's time for a change. We need a smarter approach that cuts down on errors by automating the process and making it easy to replicate, saving us both time and headaches.

Now imagine you're trying to keep 20 virtual machines perfectly aligned across different stages: development, testing, staging, and then finally, production. Sounds tricky, right? It's like trying to keep a group of fast-moving kittens in a single file - definitely not a simple task! This becomes even more complex when someone sneaks in a change, and you're left without a breadcrumb trail to follow because the documentation (if it's even there) hasn't caught up.

It's a common challenge that many businesses face. Ensuring that everything is consistent and can be traced back through different infrastructures are the urge need and solid foundation for robust operational practices.&#x20;

This is the example of the simple compute instance.As we delve into handling storage, databases, networks, and Kubernetes, the complexity escalates, presenting significant challenges beyond what traditional methods can comfortably address.

### Common challenges

* Time-Consuming Procedures: The conventional approach often involved time-consuming processes, particularly when provisioning multiple servers simultaneously.
* Proneness to Errors: Human errors during manual configurations were frequent, posing a risk of misconfigurations that could compromise the security and performance of the infrastructure.
* Inconsistency in Setup: Each server was set up individually, creating a challenge in maintaining uniformity and consistency across the entire infrastructure.
* Complexity in Manual Configurations: Configuring intricate network architectures manually heightened the chances of errors, making the overall management of the infrastructure more challenging.
* Insufficient Documentation: Changes implemented through graphical user interfaces (GUIs) often lacked comprehensive documentation, making it difficult to comprehend and replicate configurations accurately.
* Scaling Difficulties: Manual adjustments were required to scale the network for increased traffic or new components, leading to delays and potential operational inefficiencies.
* Dependency on Individuals: Deployment processes were often reliant on specific individuals who possessed the knowledge of the steps, resulting in a single point of failure in case of their unavailability.
* Limited Rollback Options: Rolling back changes in case of issues proved challenging, as there was no standardised process for versioned deployments, hindering effective troubleshooting.
* Communication Gaps: Absence of collaboration tools and version control systems led to communication gaps between teams, causing conflicting changes and potential disruptions.
* Audibility Challenges: Tracking the origin, timing, and reasons behind specific changes was challenging, making it difficult to conduct thorough audits and troubleshoot issues effectively.
* Risk of Data Loss: Accidental changes or deletions without proper backups posed a significant risk of data loss and potential disruptions in service availability.
