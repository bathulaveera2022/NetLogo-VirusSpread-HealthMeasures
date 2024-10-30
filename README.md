Project Title: NetLogo-VirusSpread-HealthMeasures-Agent Based Modeling
This project, NetLogo-VirusSpread-HealthMeasures, is designed to simulate virus spread dynamics across two distinct populations, exploring how various health measures impact infection rates, immunity development, and overall population health. Using NetLogo, an agent-based modeling environment, the simulation captures the interactions among individuals with distinct group characteristics and their response to different health interventions.
Project Overview
The main goal of this model is to examine the impact of health interventions on infection dynamics, immunity formation, and mortality rates across two simulated populations. Each population has its unique characteristics, with variations in infection susceptibility, antibody response, and density. The model simulates factors like travel restrictions, social distancing, and self-isolation, providing insight into how each measure affects virus spread and population resilience over time.
Agent-Based Modeling in Artificial Life with Robotics
Agent-based modeling (ABM) in artificial life and robotics is a powerful approach to studying complex systems through the simulation of individual agents and their interactions. This methodology is particularly valuable in exploring how simple rules at the agent level can lead to sophisticated collective behavior, akin to those seen in biological and social systems.
In this project, ABM is utilized to simulate virus spread within a virtual population, where each individual is an agent with distinct characteristics such as infection status, immunity, and group affiliation. This setup models how a virus could spread and be mitigated through various health measures like social distancing, self-isolation, and travel restrictions. By tracking the interactions between agents and their environment, the model provides insights into the effectiveness of each health measure on reducing infection and mortality rates in distinct populations (e.g., pink and gray populations).
In robotics and artificial life research, ABM extends to include embodied agents that can interact physically or virtually, mimicking real-world scenarios like disease control, environmental adaptation, or resource competition. Robotic agents with defined behaviors—modeled here as turtles with properties like movement, infection, and immunity—enable researchers to observe how adaptive or programmed rules impact outcomes. For example, virtual agents could represent drones or autonomous robots that need to self-isolate or collaborate under specific conditions, allowing us to extrapolate findings to robotic applications.
The insights from this model extend beyond virus spread to other scenarios in artificial life, where agents might interact under constraints, leading to emergent behaviors. This makes ABM a fundamental tool for understanding collective dynamics in fields ranging from epidemiology to autonomous robotic systems, providing a scalable way to test and iterate on strategies within controlled, repeatable environments. This project therefore demonstrates how agent-based modeling serves as a bridge between biological phenomena and engineered systems, enabling meaningful applications in fields that rely on complex, adaptive interactions.

Core Components of the Model
The simulation includes a few key components:
1.	Populations:
o	The model divides individuals into two groups, a “pink” and a “gray” population. Each group has its own density, initial immunity levels, and infection susceptibility.
o	Agents in each group have specific attributes, including antibody count and infection duration.
2.	Health Measures:
o	Social Distancing: Reduces the likelihood of infection spread through decreased agent interaction.
o	Self-Isolation: Agents who are infected stay isolated, which limits the number of new infections.
o	Travel Restrictions: Limits the movement of agents across areas, influencing transmission rates within each population.
3.	Disease Dynamics:
o	The model incorporates several parameters, such as infection rate, survival rate, immunity duration, and illness duration.
o	Each infected agent has a set duration of illness, after which they either recover with immunity or die.
Model Functionality and Variables
The model’s structure includes several key variables to monitor infection and immunity changes over time:
•	Total Infected Percentage: Tracks the percentage of agents currently infected.
•	Antibody Levels: Monitors the number of agents with immunity.
•	Mortality Rate: Tracks death counts within each population to determine which population is most affected.
Analysis Functions
To understand the effectiveness of each measure, the model includes an analysis function, my_analysis. This function assesses which health intervention is most and least effective based on metrics like infection rate and mortality. It calculates various rates, such as:
•	Infected and Immunity Rates: Determines the percentages of infected agents and those with antibodies in each population.
•	Effectiveness of Health Measures: Rates each measure based on how well it controls infections and supports immunity. For example, if self-isolation is combined with social distancing and shows a reduction in infection spread, it is deemed the most effective measure.
The model also assigns the measure with the least impact on controlling the virus as “least effective,” allowing users to compare various interventions and understand which has the most significant effect.
Plotting and Visualizations
Several plots help track model progress and visualize outcomes over time:
•	Total Infected Over Time: Shows infection growth within each population over time.
•	Effectiveness of Health Measures: Displays the relative effectiveness of each health measure by tracking how infection rates fluctuate with the implementation of each measure.
•	Mortality Rates by Population: Indicates which population has the highest mortality rate, helping identify vulnerable groups.
Each plot includes specific pens to track the effectiveness or spread of the virus and plots data points across ticks (representing time). The X-axis represents simulation time, while the Y-axis displays relevant measures like infection percentage or measure effectiveness.
Insights and Potential Applications
This project provides valuable insights into how public health measures influence virus spread and immunity development. By adjusting parameters, users can simulate different infection scenarios and observe how well each measure performs in containing the virus. For instance, the model can simulate conditions with high travel restrictions, low social distancing, or prolonged illness duration, helping users understand which combination of measures might best reduce infections and mortality.
Conclusion
The NetLogo-VirusSpread-HealthMeasures model serves as a tool to explore and visualize the effects of various health interventions on viral spread. With customizable settings and interactive plots, this model can support educational and research efforts by illustrating the complex dynamics of virus transmission and the importance of well-planned health measures.

