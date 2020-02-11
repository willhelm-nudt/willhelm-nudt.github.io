# Abstract

Investigates the question of how to offer flexibility and efficiency as well as strong security in cloud infrastructure. This project addresses two important platforms in cloud infrastructures:the containers and the IaaS.Iaas suports secure sharing of cloud resources among mutually untrusted users,but does not provide sufficient flexibility and effiency.Many powerful management primitives enabled by the underlying virtualization platform are hidden from users,such as live virtual machine migration and consolidation.

Library Cloud is a new abstraction that enables more flexible and efficient user-level cloud resource management without breaking security isolation between different users.Together,these systems represent important steps towards secure,flexible,and efficient cloud infrastructure.

Flexibility refers to the support of user customization on cloud services and resource management policies.

Efficiency refers to the capability of improving performance and reducing cost of resources including hardware,energy,man power,mony and time.

Security means the protection of user computation and resource against unauthorized access,data leakage,and malicious attacks or damages.

With  the ExoKernel mathod,the new type of OS can be structured with two layers.The lower layer,which is called the protection layer,multiplexes resources and focuses only on protection and security isolation,while the upper layer,which is called the management layer,is composed of management components that we dedicated to each tenant of resource manangement.

Benefits:

Security:simple and small protection layer,security isolation is easier to verify and maintain.

Flexibility:applications have the freedom to customize them for their own purpose without affecting others or compromising security isolation.

Efficiency:The dedication of the management layer eliminates the requirement of implementing security isolation,enabling many performance optimization opportunities that are hard to implement when isolation is required.

**Limitations**

The protection layer does not provide high-level abstractions.Mutiple management components need collaboration to maintain a consistent and secure abstraction,which increase system complexity.

Anothor problem is that security isolation boundaries among different management components can incur performance overhead.Further research is required to provide a general guideline for addressing the trade-off.

#Library Cloud

**Abstraction**
LC abstraction is conceptually similar to Library OS:users and applications get control over a full cloud software stack and can custmoize it for their own purpose;the underlying cloud provideers only need to provide basic resource multiplexing and isolation.The LC extends the notion of Library OS:a single Library Cloud can span across multiple cloud providers.

Applications running in a Library Cloud interact using a _Library Cloud API_ that can be much richer than a typical cloud API.Typical Cloud API methods include creating VMs and managing networks,extensions include live VM migration,consolidation,checkpointing,and dynamic scaling.
### Innovations Enabled by the LC
**Follow the Sun**

**Dynamic Resource Scheduling**

_Supercloud Dynamic Resource Scheduling_ minimize cost without compromising applications performance or changing application configuration.
_SDRS_ 
实现了虚拟机监视器级别的机制，包括VM迁移，CPU capping，memory ballooning,page sharing.I/Othrotting，提高了资源贡献效率，还保证不同的VM不会影响到彼此。当负载增加是，嵌套VM迁移到独立的VM来为更强大的应用提供支持。

##Smart Spot Instance

将VM迅速迁移到最便宜且最可用的地点。

## Super Cloud

### Computing

**Nested Virtualization**
