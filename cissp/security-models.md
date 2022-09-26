
## Security Models



### State Machine Model
Is a system that is always secure no matter what state it is in, based on a finite state machine.

### Information Flow Model
Focuses on controlling the flow of information. Information flow models are based on the state machine model.

### Noninterference Model
Is loosely  based on the information flow model. It is concerned with how the actions of a subject at a higher security level affect the system state or the actions of a subject at a lower level.

### Take-Grant Model
Employs a directed graph to dictate how rights can be passed from one subject to another or from  a subject to an object.
* **Take rule**: Allows a subject to take rights over an object
* **Grant rule**: Allows a subject to grant rights to an object
* **Create rule**: Allows a subject to create new rights
* **Remove rule**: Allows a subject to remove rights it has

### Access Control Matrix
Is a table of subjects and objects that indicates the actions or functions that each subject can perform on each object.

### Bell-LaPadula Model
Based on multilevel security policies. The model prevents the leaking of classified information to less secure clearance.
* **The Simple Security Property**: A subject may not read information at a higher sensitivity level
* **The * (star) Security Property**: a subject may not write information to an object at a lower sensitivity level (no write-down/confinement property)
* **Discretionary Security Property**: The system uses an access matrix to enforce discretionary access control.

### Biba Model
Focuses on integrity. The biba model is also built on state machine concept. Based on infirmation flow, and is a multilevel model.
* **The Simple Integrity Property**: Subject cannot read an object at a lower integrity level (no read-down)
* **The * (star) Property**: A subject cannot modify an object at a higher integrity level (no write-up)

### Clark-Wilson Model
uses a multifaceted approach to enforcing data integrity. Instead of defining a formal state machine it defines each data item and allows modifications through a controlled interface.
* **CDI** Constrained Data Item is any data whose integrity is protected
* **UDI** Unconstrained Data Item is any data whose integrity is not controlled
* **IPV** Integrity Verification Procedure is a procedure taht scans data items and confirms their integrity
* **TP** Transformation Procedure are the only procedures that are allowed to modify the integrity

### Brewer and Nash Model
Created to permit access controls to change dynamically based on a user's previous activity

### Goguen-Meseguer Model
Is an integrity model (said to be the fundation of noninterference). It is based on predetermining the set or domain of objects that a subject can access.

### Graham-Denning Model
Is focused on the secure creation and deletion of both objects and subjects
* Create / Delete objects and subjects
* Provide: read, grant, delete and transfer rights

### Harrison-Ruzzo-Ullman Model
Focuses on the assignment of objects access rights to subjects. It is an extension of the Graham-Denning Model