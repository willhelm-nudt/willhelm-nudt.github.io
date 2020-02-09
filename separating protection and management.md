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
