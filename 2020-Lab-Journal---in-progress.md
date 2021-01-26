---
title: "2020 Lab Journal"
author: "Kelly Mistry"
date: "7/24/2020"
output:
  html_document: 
    keep_md: yes
---




### C++ course 

C++ introductory course from Codecademy is 61% completed. Notes from the first 5 sections (hello world, variables, conditionals & logic, loops and vectors):

* possible variables types are: int for integers, double for floating-point numbers, char for individual characters, string for sequence of characters, and bool for true/false
* for loop format is a little different from R, with the counter declared, the bounds of the counter and the interval of the counter in 3 separate parts. Ex: for (int i = 0; i < vector.size(); i++) {operation}. The i++ means the counter advances by 1. 
* if else is very similar to R in terms of syntax
* using vectors requires adding the vector library at the top of the script with #include <vector>, and the type of variable in the vector is declared when the vector is created. Ex: std::vector<int> vector_name = {vector contents}
* to print both variables, plain text and have a line break: std::cout << variable_name << "text" << "\n"; 

**Cheatsheets for all of the course contents are here: https://www.codecademy.com/learn/learn-c-plus-plus/modules/learn-cpp-hello-world/cheatsheet**


Notes from Functions section:
* similar structure for R functions, but parameter types and return value type needs to be explicitly define: return_value_type function(parameter_1_type parameter_1, parameter_2_type parameter_2) { function operation }



### Applied Time Series Analysis course materials

Working through Applied Time Series Analysis course materials. 


#### Section One

No issues with the first section, on matrix manipulation in R. 

One cool function I hadn't come across before is diag(), which creates a matrix with zeros except on the diagonal, which is the values you put in diag(); one value means all diagonals will be that value 1, 0, 0, 0, 1, 0, 0, 0, 1, or you can specify each value in the diagonal: 1, 0, 0, 0, 2, 0, 0, 0, 3. 



#### Section Two 

Linear regression in matrix form, was mostly also a review of concepts I already knew. 

Notes
* not sure I completely understand what matrix form 2 is used for; is it for mixed effects models? I understand how the math works, just not completely clear on the functionality - it is purely used for time series?



#### Section Three

Intro to time series - should definitely be just a review

* Time series are characterized by being an ordered data set, with autocorrelation of some kind
* model time series as a combination of trend (m_t), seasonal component (s_t) and remainder (error or noise; e_t); x_t = m_t + s_t + e_t
* types of trend: moving average (easily scalable)
* once you have an estimate for trend, find s_t by using s_t = x_t - m_t (in this scenario, s_t actually includes e_t)
* once you have s_t, e_t = x_t - m_t - s_t; not sure I totally understand this, if the s_t above was s_t + e_t, essentially. I guess you use all of the x_ts to estimate a mean s_t and then use that? Looks like this is the case, yes.


#### Section Four





### Indigenous Statistics book notes

Book about Indigenous quantitative research methodology by Maggie Walter and Chris Andersen, (2013)
p. 7
* "Population statistics in particular are an evidentiary base that reflects *and* constructs particular visions considered important in and to the modern state. They map the very contours of the social world itself." 
* choosing both what is included AND what is excluded in a nation's population data constructs the nation's vision of itself. An example of this is automatically designating a male adult in a household as the head of house and a female adult as a dependent in the US census up until the 80s. 
p. 8
* population statistics is the primary way that western nations "know" about their indigenous citizens, and are assumed to be objective representations of reality. 
* increasingly, statistics is how Indigenous people understand themselves and their communities as well. 




### Notes on Thorson, 2019: Guidance for decisions using the Vector Autoregressive Spatio-Temporal (VAST) package in stock, ecosystem, habitat and climate assessments

* it's challenging to communicate across models and review standards for fisheries scientists, and spatio-temporal models provide a "common currency" to bridge these communication gaps
* scientists in the US have been increasingly entrusted with large roles in policy making (Magnuson-Stevens Act is a big reason, because it requires biological information to be part of fisheries management activities, including "setting upper limits on allowable catch, identifying the likely impact of ecosystem components on optimal yield, and the designation of essential fish habitat."
* different types of models were developed in order to measure different biological quantities, the most common being maximum sustainable yield (stock assessment), impact of species interactions on productivity (ecosystem assessment), richness and productivity of different locations (habitat assessment), and likely impact of climate change on productivity (climate assessment). 
* all of these can be estimated by developing a model that tracks how population density of one or more species at multiple locations within an ecosystem changes through time, which can be done with spatio-temporal models
* spatio-temporal models estimate variation in one or more response variables across multiple locations and time periods; they follow a state-space model tradition of incorporating both process variability and measurement errors in fisheries models but also account for the "Law of Geography": spatial correlation of process and/or measurement errors 
* VAST has been shown to be a useful single package that can be used for multiple assessment types, and allows for sharing expertise and standards across teams
* Thorson wrote this paper in order to instruct everyone on how to use this package so it can be standardized, with case studies to demonstrate
* Two different tutorials with annotated code can be found here: www.github.com/james-thorson/VAST/examples)
* VAST model equations and links to the R interface can be found here: www.github.com/james-thorson/VAST/manual
* VAST was originally developed for fisheries off the US West Coast: "The Northwest Fisheries Science Center uses a spatially-stratified bottom trawl survey to sample groundfish densities for this region (Keller et al., 2017)". This survey produces an "index of abundance" intended to be proportional to biomass for many species, which then has a stock assessment model fitted to each abundance-index to estimate population density changes over time
* The abundance-index has had to be model-based because of differences in equipment between survey vessels, which affects catchability (so raw data wouldn't be comparable)
* they were using an R package called nwfscDeltaGLM to create these model-based index standardization, and they had research indicating that treating the interaction of spatial stratum and year as a random effect was robust in terms of "spatial variability" (does this mean habitat variation across a unit of space? Or just any kind of variation between strata? Or maybe variation of population within a strata?) and low sample sizes in some strata. However, using this technique still required defining spatial strata "a priori" ("relating to or denoting reasoning or knowledge which proceeds from theoretical deduction rather than from observation or experience" - making uninformed strata decisions, basically), and didn't include information about which strata were next to one another
* In an attempt to address these two issues, Shelton et al. (2014) tried a spatially-explicit model and found that it explained a lot of residual variation "by accounting for variable population density within existing spatial strata" but this method took a long time to run the model
* VAST grew out of several packages, including from Kristensen et al. (2014), which produced the Template Model Builder (TMB) package for mixed-effects models, and the R-INLA package (Illian et al., 2012), which used stochastic partial differential equation approximation (SPDE) for spatio-temporal processes. Thorson et al. (2014b) efficiently implemented SPDE approximation with TMB, and introduced a new package SpatialDeltaGLMM that produced single-species index standardization models with either spatio-temporal effects or just spatial effects. At the same time, spatial factors analysis was introduced (Thorson et al. 2015b), used for estimating covariation for multiple species in a single time interval (Spatial_FA), and the next year they expanded this to account for both spatial and spatio-temporal covariation (SpatialDFA). In 2017, Thorson and Barnett merged all features of SpatialDeltaGLMM, Spatial_FA and SpatialDFA into a single R package, VAST
* VAST also includes features from MIST, a package that estimates species interactions
* More features continue to be added, but with the intention that it will always be backwards compatible, so old code should always run with no or minimal modifications
* VAST has mostly been used in stock assessments so far, not ecosystem or climate assessments, but that may just be reflective that these analyses are done less often and VAST has only been around for a few years. 
* Applications of VAST for fisheries management have only occurred in the Gulf of Alaska, Eastern Bering Sea, US West Coast and South Africa so far.
* Four main design principles: **area weighting** (estimate variables occurring over a pre-defined spatial domain; it "predicts population density for all locations within this spatial domain" and then anything derived from that prediction is done with weighting density estimates by the area associated with the estimate), **distinct catchability and habitat covariates** (these need to be separate because only habitat covariates are used to predict population density within the spatial domain. By doing this, VAST "controls for" i.e. filters out catchability covariates and "conditions upon" i.e. uses info from habitat covariates to improve performance with population density prediction. Previous index standardization methods used a year intercept and treated it as the abundance index, which made all other covariates as "catchability covariates"), **condition on missing covariates** (), **bridge between univariate and multivariate applications** ()
* 





## 12/10/2020 VAST tutorial notes 
* KEEP TRACK OF WHICH VAST RELEASE & CPP MODEL FILE VERSION I AM USING when I start actually working on the project code
* if you have both CPUE and AreaSwept_km2, make all AreaSwept_km2 = 1 so it doesn't account for it twice (CPUE isn't required, AreaSwept_km2 is enough)
* include a column called "Pass", with all 0 values (it can break without this, but no one Cecilia knows uses it, and she doesn't know what it would be used for anyway)
* I'll probably need to do my own area extractions (instead of using something already loaded in VAST) because of the patchy nature of the trawl area (untrawlable parts and areas more than 700 m deep typically aren't trawled, so I don't want to try to extrapolate into these areas) - Region = "user" tells it I'll be giving it a custom area, and then strata.limits = my_area is where my custom area will be called
* n_x = 500 for 500 knots for spatial analysis - this should be fine 
* make_settings() is the function that sets all of the VAST settings 
* I'll want purpose = "index2" (sets a bunch of default settings in order to tell VAST to do an abundance based on index data so I don't have to go through and set a bunch of settings manually)
* bias.correct = TRUE is a final setting I'll want, but it adds a lot of computation time, so turn this off when I'm messing with things and just turn it back on for the final run
* use_anisotropy = TRUE is a setting that will take direction into account when calculating autocorrelation, which makes sense in the context of Gulf of Alaska habitat heterogeneity
* in the fit_model function, "input_grid" is for my custom extrapolation grid, which Cecilia already has a .csv file for and code to turn it into the correct format
* for environmental covariates, I can choose non-linear relationships (parametric being a likely choice for some covariates), and they can effect either the encounter probability, the density if encountered, or both (a situation where it is effecting encounter probability but not density, but it could be effecting density but not encounter)
* correlation of environmental covariates is something to look for before using VAST; if there are highly correlated covariates, then use one at a time in VAST and see how much variation is explained by each
