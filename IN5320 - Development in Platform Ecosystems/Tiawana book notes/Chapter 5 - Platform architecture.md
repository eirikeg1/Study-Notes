
# Content summary
---

* The two gears of platform architecture (architecture/government)
* How complexity paralyzes innovation in ecosystems
* How Architectures reduce complexity
* Two functions of architecture: 
	* **Partitioning**
	* **Reintegration**
* Two facets of ecosystem architecture: 
	* **platform architecture** 
	* **app microarchitecture**
* Four desirable properties of platform architectures
* Modularization
* Two mechanisms for modularizing architectures:
	* **Decoupling**
	* **Interface standardization**
* Simple rules for what goes into the platform and what stays out
* Tradeoffs in architectural choices

# Two gears of PE
---

* The two gears are architecture and governance
* These need to be aligned with each other to ensure the effective evolution of ecosystem
* **Architecture** refers to the technical design and structure, including how the platform is partitioned into a stable core and a complementary set of apps
* **Governance** encompasses the rules, policies and mechanisms through which the platform owner manages and controls the ecosystem, including interactions with and between app devs and other stakeholders
* The alignment is crucial because each influences the effectiveness of the other.

### Two types of complexity

#### Structural complexity
_Complexity of the architecture of the ecosystem itself - the way its various parts are interconnected_

* The _skeleton_ of the system
* Related to number and nature of the connections between the platform and it's complementary apps, and its interdependencies.
* How many components, how they are connected

#### Behavior complexity
_Unpredictability of the aggregate of the components withing the ecosystem - how they behave according and in relation to each other_

* The dynamic and often unpredictable interactions and outcomes that emerge from the functioning of this structure
* Not just about structure or components itself, but interaction between them
* Can include dynamics of competition and cooperation among app developers, the way users engage with the platform and its apps, and how changes in one part of the ecosystem can affect others in unforeseen ways

# Complexity paralyzes innovation
---

* Complexity is is the main challenge which stifles platform ecosystems, described as 'The Archilles heel of platform ecosystems
* Two main challenges: Incomprehensibility and gridlock
* These challenging can be reduced by reducing the complexity of the platform

### Incomprehensibility
_First challenge of complexity, where understanding the whole platform might be a challenge_

* As a PE grows, it becomes increasingly difficult for any one person to fully comprehend its entirety. 
* This complexity can stretch beyond the cognitive abilities of human understanding, making it challenging for platform architects to fully grasp the technology they are creating
* App developers may also struggle to understand the complexity of the ecosystem in which their apps must function

### Gridlock
_Second challenge of complexity, where changing one component might either change/break a lot of other functionality or not affect anything else at all_

* High complexity can become overwhelming that it can lead to a form of paralysis, where making one small change might not be good.
* Minor changes might trigger unpredictable ripple effects throughout the ecosystem

# The two functions of Ecosystem Architecture
---

* The two functions together are essential to the design and operation of the PE
* They help balance the need for independent development and innovation in individual components with the necessity of maintaining a coherent and functional overall system

# Partitioning
_Decomposition of the ecosystem into manageable and distinct components_

* Separating into platforms core infrastructure from it's various apps or services.
* By doing so, each component can be developed, operated and managed independently.
* This separation facilitates specialized development and innovation, as each component can focus on its specific function without being hindered by the complexities of the entire system.

# Systems integration
_Once ecosystem is partitioned, these components need to be effectively integrated to ensure smooth operation and interaction_

* Is about establishing and maintaining the connections and interactions between platforms core and its complementary apps.
* This includes defining how they communicate, share data, and coordinate activities.
* Effective integration is crucial for ensuring that the overall platform ecosystem functions cohesively and efficiently, despite the autonomy of its individual components.


# Two facets of ecosystem architecture
---
_Two different sides of how the design of the overall architecture is designed_

# Platform Architecture
_Overall design and structure of the software platform itself_

* Includes core infrastructure and functionalities that are central to the platforms operation.
* Dictates how the platform is built, how it interacts with various apps and how it supports them
* This architecture is crucial for ensuring stability, scalability, and efficiency of the platform
* Typically involves decisions about modularity, interfaces and integration points


# App Microarchitecture
_The internal design and structure of individual apps that operate within the platform ecosystem_

* Deals with how an app is built to interact with the platform and other apps
* Includes decisions about how the app's various components (like presentation logic, application logic, data access logic, etc) are organized and how they communicate with the platform
* Effective app microarchitecture ensures that apps can leverage the platform capabilities while maintaining their independence and unique functionality


# The four desirable properties of platform architectures
---
_Architectural properties which always invokes tradeoffs such tat dramatically increasing one property will reduce another (Tiawana 93)_

## Simplicity
_Architecture should be simple enough to be understood at a high level of abstraction_
* The main components, their partitioning and how they interact should be easily comprehensible
* Helps in managing and evolving the platform

## Resilience
_One malfunction in the app should not cause the entire ecosystem to malfunction_
* Usually achieved through loose coupling of apps with loose coupling of apps with the platform, thereby preventing cascading failures

## Maintainability
_architecture should support cost-effective changes without breaking other components_
* Includes both the ability to make changes within the platform and ensuring that changes in one app do not require parallel changes in the platform or other apps.
* Helps in adapting to new requirements and technologies over time.

## Evolvability
_Architecture should support the platforms evolution over time_
* It should be adaptable to changes in technology, market demands and user needs.
* Evolvability is crucial for the long-term viability and competitiveness of the platform.


# Modularity
---
_General property of any complex system, where it can be decomposed into smaller subsystems that are always going to be interdependent to some extent. This modularity _

## 5 useful lessons from screwdriver example

1. Makes its production divisible among many organizations (partitioning) 
2. Restricts their interdependence to its connection points (interfaces)
3. Relies solely on compliance with interface specifications to integrate the four organizations’ outputs (systems integration) 
4. Sacrifices some performance for future flexibility (the so-called modularity tax) 
5. Allows unforeseeable capabilities to be added in the future (emergent properties)

## Software modularity
_The degree to how much a systems components can be separated and recombined. How monolithic_
* Facilitating independent development and innovation
* Scalability
* Simpler maintenance updates
* Allows components (like apps) to be developed, operated and updated independently, enhancing the platform's flexibility and adaptability

## Platform architecture is like an ecosystem's DNA
_Almost impossible to change it in practice_
* Architecture dictates how platform operates, interacts with the apps and how adaptable it is to changes
* Underscores the importance of getting the architecture right from the outset, as later changes can potentially be extremely challenging

## Design precedes production
_Design phase is crucial and precedes production_
* Design of platforms architecture dictates how various systems will interact, integrate and function.
* Critical for future effectiveness, efficiency and future adaptability of platform

## Design modularity enables production modularity
_Modularity in design phase enables modularity in the production phase_
* When a platform is designed with modular principles, it also allows for modular production.
* Modular production allows for independent development, testing and deployment of component.
* This modularity allows for the platforms ability to evolve, adapt and scale over time.

# Upsides of modularization
![[Pasted image 20231212163507.png | 650]]
### For platform owners
* Massively distributed innovation
* Increased variety of apps
* Control via architecture rather than ownership
* Greater volume of incremental and app-level innovation
	* Accelerates the quantity of innovation in the lower two cells in FIGURE 5.19
	* The more modular, incremental tweaking turns more into modular innovation-oriented
	* Simplified coordination between developers, through design parameters and interface specifications instead of direct communication
	* New apps can rapidly extend the platform's own capabilities, and the threshold for minor changes is heightened
	* ![[Pasted image 20231212164419.png|500]]
* 
### For app developers
* Less reinvention, more specialization
* Valuable ignorance
* Greater app evolvability
	* Less risk for ripple effect
	* Free to innovate as you wish, within the platforms interfaces and constraints
* Multihoming in rival platforms more feasible
	* Rival platforms are more likely to share some common features, which app developers are less likely to reinvent

# Downsides of modularity

![[Pasted image 20231212165706.png | 650]]

* Modular architectures should be favored when rapid innovation is more important than overall performance.
## For app owners
* Modularization is not free for platform owners. Cost substantial upfront costs of modularizing  and establishing interfaces.
* Technical performance take a hit
	* Monolithic architectures usually can outperform modular ones in the short run, but lead to rigidity because they are hard to change in small increments
	* Might split functionality that should not be split
	* Less tailored functions
* Forecloses architectural innovation
	* The freezing of platform interfaces for modularization can lock in the platform for a substantial period, even when superior alternatives become available​​.
* Increased risk of imitation from rivals
	* Easier to understand and faster to develop

![[Pasted image 20231212171420.png | 500]]

## For app developers

* Modularity imposes additional costs
	* Upfront costs of compliance with design rules and interface specifications for app developers.
* Technical performance takes a hit
	* Due to the division of functionalities across multiple subsystems and the increased need for inter-subsystem communication
* Modularity contrains experimentation
	* Can limit developers freedom to experiment and utilize new technologies
* Leveraging the platform risks getting locked into it
	* Developers who heavily  utilize a particular platforms modular architecture risk becoming overly dependent on it, potentially limiting their ability to operate across different platforms or adapt to new technologies


# Two mechanisms for modularization
---
# Decoupling
_Decomposition of the ecosystem into relatively independent apps_

![[Pasted image 20231212173228.png | 500]]

* Decoupling is accomplished through encapsulation
* Minimizes the need for app developers in its ecosystem to have to know hidden or unimportant information for their use case
* Interacting with platform should not require anything else than it's interface
* Requires creating and maintaining partitions of design information into hidden and visible subsets.

## Decomposition by reusability and variability
_Partition PE into stable and variable blocks as well as high- and low-reusability blocks of functionality_

* Requires evaluating each major element of functionality for inclusion in or exclusion from the platform core.
* Two guiding principles:
	* *Economies of scale across the ecosystem*
	* *Reduced costs of developing apps for the platform*

#### 5 magic rules for platform ecosystems
1. *High-reusability functionality goes in the platform*
	* Subsystems that are highly reusable and shared by many apps should be part of the platform.
	* Allows for rapid improvement of these functions due to their co-location and tight integration with the platform.
	* Even though platform in it self is externally modular, it can be internally monolithic
2. *Generic functionality goes in the platform*
	* Functions which are generic enough to be useful for multiple apps should be included
	* Encompasses common components and functionalities shared by many app implementations
	* Platform owner may choose to control certain functionalities for strategic reasons, but functions specific to few apps should be implemented as apps and kept out of the platform.
3. *Any interfaces to the platform are an integral part of the platform*
	* Both core codebase and interfaces are considered inseparable parts of the platform
4. *Stable functionality goes into the platform
	* Immature, changing or evolving functionalities are better suited to be implemented as apps
5. *Functionality with the highest uncertainty remains outside the platform*
	* Where multiple solutions are viable should be left outside
	  * Allows for diverse experimentation and avoids premature commitment
	  * Market will eventually determine the most successful solution among the competing apps
	  * Two exceptions to this rule:
		  1. A platform owner should integrate functionality that is deems critical to the attractiveness of the platform to end users
		  2. A platform owner should include functionality in the platform that it deems critical in terms of end-user expectations and norms set by rivals

## Decoupling by specifying allowable assumptions
_Platform owner can explicitly specify assumptions that an app can make about the platform, and what assumptions the platform can make about the apps_

![[Pasted image 20231212175527.png | 500]]

### Key aspects

#### Reduced interdependencies
_Primary goal is to minimize the dependencies among the subsystems_
* By specifying what assumptions are permissible, it limits the degree to which changes in one subsystem (like platform core) directly impact the functioning of another subsystem (like individual app)

#### Explicit assumptions
_Assumptions that are allowed are explicitly stated_
* This clarity helps app developers understand the extent to which they can rely on the platform's functionality and, conversely, helps the platform designers understand the extent to which they should cater to the app's needs.
* Reduces the risk of over-dependence on specific platform functionalities or app features

#### Facilitates modularity
_This approach supports a modular architecture within the platform ecosystem_
* By delineating clear boundaries and interfaces, it allows for the independent development and evolution of the platform and its apps
* This modularity is critical for scalability, adaptability and the facilitation of innovation within the ecosystem

#### Balancing flexibility and control
_While providing a framework for app developers to understand their limits and possibilities, it also gives the platform owner the ability to maintain a degree of control over system_
* Balance is essential to ensure that the platform remains stable and viable while allowing app developers enough freedom to innovate and add value

#### Stability and evolution
_By specifying allowable assumptions, the platform can maintain a stable interface with apps while internally evolving_
* Allows for ongoing improvement and adaptation of the platform's core functionalities without necessitating constant adjustments by app developers


# Interface standardization
_Interfaces should follow specific set of rules_
#toExpand 

## Precisely documented
_All information about an app must communicate and interact with the platform is explicitly documented_
* Must clearly lay out the rules for how and the platform communicate, interact and exchange information
*  Should explain how to interoperate with the platform independently of the app's internal implementation
* Defined and well specified

## Frozen standards
_Once documented by the platforms owner, interface standards should not change over time_
* Provides stability and predictability for app developers
* Does not break old implementations
## Versatile
_The more general a standard, the more versatile_ #Maybe 

![[Pasted image 20231212185344.png|500]]


# Rules for what goes into/stays out of the platform #redundant
---

* Guidelines for deciding which functionalities should be included in a platform's core and which should be left for individual apps to implement
* Vital for maintaining a healthy balance between the platform's core capabilities and the ecosystem's overall flexibility and innovation potential
* Exceptions to these rules occur when platform owner deems specific functionalities critical for the platforms attractiveness or necessary to meet user expectations shaped by rival platforms

1. High-reusability functionality goes into the platform
	* Rapid improvement
	* Platform can be monolithic internally but modular internally
2. Generic functionality goes into the platform
	* Functions which are generally useful across a wide range of applications
	* Specific functionality from rivals may also be included
3. Platform Interfaces are integral to the platform:
	* Both core codebase and the interfaces of the platform are considered essential components of the platform due to their high reusability and long lifespans
4. Stable functionality goes in the platform:
	* Functionality which is stable and less likely to change or evolve rapidly should be prioritized
	* Other functions should be left for apps
5. Functionality with high uncertainty stays out
	* Functions where best solution is not clear, or multiple viable solutions
	* Encourages diverse experimentation by app devs
	* avoids premature commitment to potentially inferior solutions
	