

# Abstract
_One of the main shortcomings of event data in football, which has been extensively used for analytics in the recent years,
is that it still requires manual collection, thus limiting its availability to a reduced number of tournaments. In this work, we
propose a deterministic decision tree-based algorithm to automatically extract football events using tracking data, which
consists of two steps: (1) a possession step that evaluates which player was in possession of the ball at each frame in the
tracking data, as well as the distinct player configurations during the time intervals where the ball is not in play to inform set
piece detection; (2) an event detection step that combines the changes in ball possession computed in the first step with the
laws of football to determine in-game events and set pieces. The automatically generated events are benchmarked against
manually annotated events and we show that in most event categories the proposed methodology achieves +90% detection rate
across different tournaments and tracking data providers. Finally, we demonstrate how the contextual information offered by
tracking data can be leveraged to increase the granularity of auto-detected events, and exhibit how the proposed framework
may be used to conduct a myriad of data analyses in football._
# Keywords 
* Football analytics
* EPTS
* Event data
* Ball possession
* Auto-eventing
* Data democratization

# Notes
---

* _To the best of our knowledge, this article represents the first attempt to use tracking data as a means to automatically generate event data._
* Decision tree based algorithm
	* 2d coords of players
	* for different events (shots, keeper, possession,...), different decision trees dictates the outcome
* 






