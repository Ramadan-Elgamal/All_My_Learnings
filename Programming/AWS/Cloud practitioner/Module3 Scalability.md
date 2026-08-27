> **Scalability** refers to the **ability of an application or system to handle increasing loads by adapting.**
> 
> - **Vertical Scalability:** Adding more resources (e.g., upgrading server hardware) to handle increased call volume.
> - **Horizontal Scalability:** Adding more call center agents to handle increased call volume, allowing workload distribution across multiple agents.


>**Vertical Scaling (Scaling Up)** means making a single server bigger. In AWS, this is like changing your EC2 instance from a small size with 2 CPUs to a large size with 8 CPUs.
- **Pros:** Very simple. Your code does not need to change.
- **Cons:** You eventually hit a limit because servers can only get so big. If that one server crashes, your whole application goes down. It usually requires turning the server off for a few minutes to upgrade it.

>**Horizontal Scaling (Scaling Out)** means adding more servers to share the workload. Instead of one huge server, you might use four smaller servers working together. In AWS, this is done using Auto Scaling Groups and a Load Balancer.
- **Pros:** You can grow almost forever just by adding more machines. You only pay for what you need because you can automatically add servers during busy times and remove them when it is quiet.
- **Cons:** It is more complex to set up. Your application needs to be designed to run on multiple machines at the same time.

### **Scalability vs Elasticity (vs Agility)**

- **Scalability:** The ability to accommodate a larger load by either enhancing the hardware (scale up) or adding nodes (scale out).
- **Elasticity:** In a scalable system, elasticity refers to the automatic scaling based on the load, enabling a pay-per-use model, demand matching, and cost optimization.
- **Agility:** Unrelated to scalability, agility implies that new IT resources can be provisioned quickly, reducing the time to availability from weeks to minutes

> **Exam Tip:** Cloud Practitioner questions often test whether you can tell these apart in a single sentence. Quick recap **Scalability** = _can_ the system grow; **Elasticity** = does it grow/shrink _automatically_ with demand; **Agility** = how _fast_ you can get new resources in the first place.