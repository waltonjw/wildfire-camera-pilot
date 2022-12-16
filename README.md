# Modeling a Fast-response AI Wildfire Camera Network in Washington State 

## Background

Wildfire activity in the western United States continues to increase in frequency and magnitude.   Today's larger and more intense fires are increasingly difficult to manage than in years past.   According to the US Congressional Research Service, the average number of acres burned per year has risen to 7.0 million acres annually.   The figure is more than double the average annual acreage burned in the 1990s.

One silver lining is that off-the-shelf technology is developing which promises to help identify wildfires when they are extremely young.   If a fire can be identified within minutes to several hours of ignition, often a rapid-strike approach can be used to fully contain the fire before it grows and requires a broader response.   This could change the way we fight wildfires.  This technology includes:

1. High resolution visible band and infrared band cameras which can capture small, distant fires via smoke plume identification or radiation detection.

2. High-speed wireless data networks such as SpaceX's Starlink or terrestrial-based 5G networks provided by companies such as TMobile, Verizon,  AT&T, and others.   Point-to-point microwave, while not a new technology, has dropped in price considerably as well and should also be included in this class of technology.
3. AI-based image and video classification engines which can automatically identify wildfires from telemetry streams, with acceptable false-positive and false-negative rates.
4. Concurrent computing infrastructure, such as services offered by AWS and Microsoft Azure which can execute image classification in real time across multiple streams and escalate potential fires to human operators in an intelligent and efficient workflows.
5. Mature GIS platforms such as ArcGIS and QGIS which can help identify optimal placement of monitoring nodes.

Organizations such as [PanoAI](https://www.pano.ai/) and [AlertWildfire ](https://www.alertwildfire.org/) are already developing and/or integrating these technologies to achieve this goal of near-instant wildfire identification and rapid response management, and more information on their efforts can be seen on their respective websites.

## Project Scope

The goal of this project is to develop a model and tools to identify a set of candidate locations for a pilot program of rapid-detection wildfire cameras across Washington State.    If phrased as a question, that questions would be:

***For a pilot program of wildfire camera tower installations in Washington State, where should they located to maximize effectiveness while minimizing installation and maintencance costs?***

This type of project could be of use to program managers tasked with planning such a network, who wish to maximize coverage footprint, minimize cost, and prioritize monitoring locations based risk, effectiveness, and expense.   The goal is to create a ranked list of locations suitable for the deployment of this technology, whether it be 1, 10, or 100 cameras.  Because this project is aimed at an initial deployment program, it is executed with several key assumptions.

1. The project assumes the use of technology which can be purchased today, including cameras, 50-foot self-supporting modular towers, commercially-available wireless data services and cloud-computing services.
2. Because a pilot program would likely have limited funds, only sites which are accessible by roads passable with 4x4 vehicles will be considered.  The idea is that a two-person crew could deploy a node, with five 10-foot self-supporting tower sections, along with camera and its associated support infrastructure such as solar panel, battery, controller, and transceiver.   A wider implementation may wish to consider more expensive installation sites which require helicopter or walk-in access and would be executed in subsequent phases.  This initial project assumes drive-in access, even if the access route is rough double-track road which requires high-clearance 4x4 vehicles with winching and recovery equipment. 

## Data Sources

The following public data sources will be used to develop the ranked list of road-accessible wildfire camera tower sites.

| Data Source                                      | URL                                                          | Purpose                                                      |
| ------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ASTER V3 Digital Elevation Model                 | https://earthexplorer.usgs.gov/                              | DEM for viewshed analysis, slope constraints, elevation constraints, and ridgeline identification. |
| BLM OR Ground Transportation GTRN Roads Line Hub | https://gbp-blm-egis.hub.arcgis.com/datasets/BLM-EGIS::blm-or-ground-transportation-gtrn-roads-line-hub | Digitized road network feature class for suitability analysis. |
| USFS Wildfire Burn Probability                   | https://www.fs.usda.gov/rds/archive/Catalog/RDS-2020-0016    | Wildfire probability raster for ranking candidate sites.     |
| MRLC Land Cover CONUS                            | https://www.mrlc.gov/data?f%5B0%5D=category%3Aland%20cover&f%5B1%5D=region%3Aconus | Ground cover type raster for area constraint.                |
| WA DNR Boundary                                  | https://data-wadnr.opendata.arcgis.com/datasets/wadnr::wa-state-boundary | Washington State boundary polygon for constraining overall analysis. |



## Methodology

This project will create the ranked list of candidate wildfire camera sites using the following basic methodology:

1. Find a subset of Washington State land with ground cover types (forests, grasslands, herbaceous, etc.), which is reasonably fire prone.   Some analysis will be needed to determine which ground cover types to include, as there are many.   This subset of Washington State will be used for further processing.
2. Using proximity tools, create a 500 foot buffer around roads.  500 feet is a reasonable distance two people could walk carrying 10-foot self-supporting tower sections one at a time.
3. Create ground slope layer to be used for finding level areas for tower construction, with ground slope less that 5%.
5. Create a minimum elevation layer to constrain candidate tower sites to higher elevation.
6. Using hydrology tools, identify ridgelines which would maximize camera scan for a given installation.
7. Using the criteria of ridgelines, ground slope, and road buffers, create a point feature class of candidate camera tower locations.  
8. Rank the list of candidate camera tower locations by running viewshed/observer points and variable fire danger.   The exact balance of each needs some further research and will be subjective.
9. Provide a final product of ranked camera tower locations along with their associated viewsheds.   Summarize the percent of high-risk lands covered by a variable number of camera tower count scenarios to help the reader understand diminishing returns.

## Expected Results

Because this project is constrained to road-accessible locations, there will likely be a sharp level of diminishing returns to the acres of land covered by each additional camera.  Washington State has some very high peaks with no road access which would make for superior tower locations, but erecting towers at these sites is vastly more expensive and dangerous than road-accessible sites.  These high-expense/high-yield locations should be saved for the production deployment after this first pilot phase has been completed.    

It is expected that a handful of candidate sites will be very suitable for a pilot deployment (i.e. a peak with 360 degree views with road access in a high-risk zone).    These will likely be near the top of the ranked candidate location list.   It is anticipated that favorable sites will drop off at a fairly high rate of diminishing returns.  
