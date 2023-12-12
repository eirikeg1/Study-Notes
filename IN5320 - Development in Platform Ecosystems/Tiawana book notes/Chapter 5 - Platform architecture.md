
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


# Notes
---

## Two gears of PE

* The two gears are architecture and governance
* These need to be aligned with each other to ensure the effective evolution of ecosystem
* **Architecture** refers to the technical design and structure, including how the platform is partitioned into a stable core and a complementary set of apps
* **Governance** encompasses the rules, policies and mechanisms through which the platform owner manages and controls the ecosystem, including interactions with and between app devs and other stakeholders
* The alignment is crucial because each influences the effectiveness of the other.

## Complexity paralyzes innovation

* Complexity is is the main challenge which stifles platform echosystems, described as 'The Archillies heel of platform ecosystems'
* Two main challenges:

## Rules for what goes into the platform and what stays out

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
	