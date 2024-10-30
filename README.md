extensions [csv]

globals [
  ;; Professor marking variables
  student_id
  student_name
  student_score
  student_feedback
  ;; Analysis variables
  most_effective_measure
  gray_antibodies_percentage
  stored_settings
  self_isolation_link
  population_density
  total_infected_percentage
  pink_infected_percentage
  gray_infected_percentage
  least_effective_measure
  population_with_highest_mortality_rate
  population_most_immune
  total_antibodies_percentage
  pink_antibodies_percentage
  avg_infection_time
  total_infected



]

turtles-own [
  antibodies      ;; Number of antibodies (number)
  group           ;; Group identifier (string)
  infected_time   ;; Duration the turtle remains infected (number)

]

;; World Setup
to setup_world
  set student_id "batthulaveera2022@gmail.com"
  set student_name "Veeranjaneyulu Batthula "
  set-patch-size 4
  resize-world -45 45 -45 45  ;; World 91x91 patches


  ;; Set patch colors using ifelse
  ask patches [
    ifelse (pxcor < 0) [
      set pcolor pink  ;; Left half is pink
    ] [
      set pcolor gray  ;; Right half is gray
    ]
  ]

  ;; Set initial global variables
  set travel_restrictions false
  set social_distancing false
  set self_isolation false
  set pink_population 1500
  set gray_population 1000
  set initially_infected 15
  set infection_rate 30
  set survival_rate 90
  set immunity_duration 260
  set undetected_period 85
  set illness_duration 290


  reset-ticks
end

;; Setup Agents
to setup_agents
  clear-turtles  ;; Clear existing agents



  ;; Setup the gray population
  create-turtles gray_population [
    set color yellow
    set size 3
    setxy random-xcor random-ycor
    if [pcolor] of patch-here = gray [
      set group "gray turtle"      ;; Set group identifier as string
      set infected_time 0          ;; Initialize infected_time as an integer
      set antibodies 0             ;; Initialize antibodies as an integer
    ]
  ]
    ;; Setup the pink population
  create-turtles pink_population [
    set color yellow
    set size 3
    setxy random-xcor random-ycor
    if [pcolor] of patch-here = pink [
      set group "pink turtle"      ;; Set group identifier as string
      set infected_time 0          ;; Initialize infected_time as an integer
      set antibodies 0             ;; Initialize antibodies as an integer
    ]
  ]


  ;; Infect initial agents in both populations

  ask n-of initially_infected turtles with [group = "gray turtle"] [
    set color green
    set infected_time illness_duration
  ]
   ask n-of initially_infected turtles with [group = "pink turtle"] [
    set color green
    set infected_time illness_duration
  ]
end





;; Run the model
to run_model


  ask turtles [
    ;; Handle infected turtles using ifelse
    ifelse color = green [
      set infected_time infected_time - 1
      ifelse infected_time <= 0 [
        ifelse random 100 < survival_rate [
          set antibodies immunity_duration
          set color black  ;; Turtle survives and becomes immune
        ] [
          set color black  ;; Turtle dies
        ]
      ] [
        ;; Turtle is still infected, continue infection logic
      ]
    ] [

    ]
  ]

  ;; Update global variables (e.g., percentages, deaths)
  update-global-variables

  tick  ;; Increment the tick counter

end




;; Update global variables after each tick
to update-global-variables
  set total_antibodies_percentage (count turtles with [antibodies > 0] / count turtles) * 100
  set pink_antibodies_percentage (count turtles with [antibodies > 0 and group = "pink turtle"]) * 100
  set gray_antibodies_percentage (count turtles with [antibodies > 0 and group = "gray turtle"]) * 100
  set total_infected_percentage (count turtles with [color = green] / count turtles) * 100
  set pink_infected_percentage (count turtles with [color = green and group = "pink turtle"] / count turtles with [group = "pink turtle"]) * 100
  set gray_infected_percentage (count turtles with [color = green and group = "gray turtle"] / count turtles with [group = "gray turtle"]) * 100
  set total_deaths count turtles with [color = black and infected_time <= 0]
  set pink_deaths count turtles with [color = black and group = "pink turtle"]
  set gray_deaths count turtles with [color = black and group = "gray turtle"]

end

;; Analysis function

to my_analysis
  ;; Variables to store the counts for each condition after running simulations
  let pink_deaths_count pink_deaths
  let gray_deaths_count gray_deaths
  let total_population pink_population + gray_population
  let pink_infected_rate (pink_infected_percentage / 100) * pink_population
  let gray_infected_rate (gray_infected_percentage / 100) * gray_population
  let total_infected_rate (total_infected_percentage / 100) * total_population
  let pink_antibodies_rate (pink_antibodies_percentage / 100) * pink_population
  let gray_antibodies_rate (gray_antibodies_percentage / 100) * gray_population

  ;; Determine Most Effective Measure
  ;; Assume 'social_distancing' as 1, 'self_isolation' as 2, 'stay_local' as 3
  ifelse (self_isolation and social_distancing and not travel_restrictions) [
    ;; Self-isolation combined with distancing
    set most_effective_measure 20  ;; Self-isolation alone is highly effective
  ] [
    ifelse (self_isolation and travel_restrictions) [
      set most_effective_measure 30  ;; Stay local (travel restriction) is more effective with isolation
    ] [
      set most_effective_measure 1  ;; Social distancing alone is moderately effective
    ]
  ]

  ;; Determine Least Effective Measure
  ifelse (not social_distancing and not self_isolation and travel_restrictions) [
    set least_effective_measure 3  ;; Travel restrictions alone are least effective
  ] [
    ifelse (not social_distancing and self_isolation) [
      set least_effective_measure 1  ;; Social distancing alone is the least effective
    ] [
      set least_effective_measure 2  ;; Self-isolation alone is the least effective
    ]
  ]

  ;; Population with Highest Mortality Rate
  ifelse (pink_deaths_count > gray_deaths_count) [
    set population_with_highest_mortality_rate 1  ;; Pink population has higher mortality
  ] [
    ifelse (gray_deaths_count > pink_deaths_count) [
      set population_with_highest_mortality_rate 2  ;; Gray population has higher mortality
    ] [
      set population_with_highest_mortality_rate 3  ;; Equally affected
    ]
  ]

  ;; Population with Highest Immunity
  ifelse (pink_antibodies_rate > gray_antibodies_rate) [
    set population_most_immune 1  ;; Pink population has higher immunity
  ] [
    ifelse (gray_antibodies_rate > pink_antibodies_rate) [
      set population_most_immune 2  ;; Gray population has higher immunity
    ] [
      set population_most_immune 3  ;; Equally immune
    ]
  ]

  ;; Identify variable with highest impact on self-isolation
  let self_isolation_impact (list pink_population gray_population initially_infected infection_rate survival_rate immunity_duration undetected_period illness_duration)
  set self_isolation_link (position max self_isolation_impact self_isolation_impact) + 1  ;; Indexing starts at 1 for this setting

  ;; Population Density Impact
  ;; Observe outcomes after 20,000 ticks with travel_restrictions enabled
  if travel_restrictions [
    ifelse (total_infected_rate = 0) [
      set population_density 4  ;; Virus dies out
    ] [
      ifelse (pink_deaths_count = pink_population) [
        set population_density 2  ;; Pink population is eliminated
      ] [
        ifelse (gray_deaths_count = gray_population) [
          set population_density 3  ;; Gray population is eliminated
        ] [
          ifelse (total_population * 0.1 > total_infected_rate) [
            set population_density 5  ;; Populations settle to similar density, virus dies out
          ] [
            set population_density 6  ;; Populations settle to similar density
          ]
        ]
      ]
    ]
  ]
end

