_Three types of models_:

# Physical models
---
* LAN 1970
* Internet 1980s-1990s
* Cloud computing 2000s
# Architectural models
---
_The logical organization of the communicating entities_
# **Components**
### **Communicating entities** 
* Objects 
* Components 
* Web services
### Communication paradigms
* Interprocess communication (IPC)
* Remote invocation
* Indirect communication
	* Information sharing through a database-like system called **MIDAS Data Space**
		* Subscribe/publish
### **Roles and responsibilities**
* Client-server model
* Peer-to-peer
* Hybrids: P2P and Client/server
### **Placement strategies**
* Multiple server processes
* Proxy servers: cache that is shared between several clients
	* Load balancers
	* Three types of cache
		* Content distribution strategy (CDN)
		* Server cache
		* Client cache
* Mobile code
	* Sending code between entities
	* **Mobile agent**
		* Used for web crawlers and web workers
		* Instead of sending a huge number of requests directly, create a separate entity to handle this. This entity can usually migrate between computers and execute a task on behalf of someone

# Architectural patterns

### Layered model
* Layers 3 and 4 can be merged as the platform layer

**Layers:**
1. Applications and services layer
	* User view and control
2. Middleware layer
	* Application logic (p2p, publish-subscribe, web services...)
	* This should be independent from the components in the other layers 
	* Context-aware and adaptive solutions (customizing the services based on their context/use-case)
3. Operating system layer
	* Database manager
4. Computer and Network Hardware layer
	* Database manager

### Tiered Architecture
_Focus on features, each feature is sort of its own stateless entity. Each feature is independent and developed independently_

* For example microservices
* Can have _n_ layers, but 3 is common

**Tiers:**
1. Presentation tier
2. Logic tier
3. Data tier

### Thin Clients
_Move complexity from end-user devices to server side_

* For example virtual computers or remote gaming

### Software architecture
### System architectures
# Fundamental models
*Models which focuses on a particular aspect of a system's behavior and abstracts over unnecessary/irrelevant details*

* The purpose is to make all relevant assumptions explicit and find out what is feasible and unfeasible based on this

# Different models
---
### Interaction model
_Model where system focuses on efficient processes, messages and coordination (synchronization and ordering)_
* The most common model
* Performance of the communication
	* Latency (delay between sending and receiving)
	* Bandwidth (total data which can be transmitted)
	* Jitter (variation of time delay between different packets)
* Computer clocks
	* How to synchronize two different entities' clocks?
	* Clock drift (rate for deviation from reference clock)
		* Systems usually fetches time from a common time system (feks GPS)
	* Ticket booking
	* Happened-before relationship

**Different Interaction model systems**:
* **Synchronous distributed systems**
	* Easier for ordered events 
* **Asynchronous distributed systems**
	* Synchronization might be unreliable

### Failure model
_Defines and classifies failures and tries to prevent or hide the failures_
* Example: TCP on top of IP to prevent and hide packet loss
* Masking a failure by either:
	* Hiding it all together
	* Converting it into a more acceptable type of failure

#### Failure types:

**Omission failure**
_Process or channel fails to perform actions that it is supposed to do_
* **Fail-stop**
* **Crash**
* **Omission**
* **Send omission**
* **Receive omission**

**Arbitrary failures (Byzantine failures)**

**Timing failures**
_Responces not available to clients in a specified time interval_
* Clock failure
* Performance failure
### Security model
* Defines and classifies security attacks
* Basis for analyses of threats to a system and to design it to resist them
