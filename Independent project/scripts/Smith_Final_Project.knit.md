---
title: "Uncovering the Secrets of Deep-Sea Microplastic Pollution"
author: "Created by Taylorann Smith" 
output: 
    html_document:
        css: bootstrap.css
        toc: TRUE
        toc_float: TRUE
---



![DeepSea](https://i.ytimg.com/vi/mlj1d5OomzY/maxresdefault.jpg)


# Passion Behind the Project
>The deep-sea remains largely unexplored, but is known to account for most of the world’s oceans. While many consider the deep-sea as far from the influence of humans, off the coast of California, deep-sea habitats are fairly nearshore in comparison to eastern coast deep-sea habitats. 

>We all are aware of the plastic crisis in our oceans, and on my deep-sea expeditions, my team has seen all types of trahs on the seafloor: tires, line, bottles, bags etc. It is also true that plastics are inorganic, and never go away, only break down into smaller and smaller pieces known as fragments and even smaller, microplastics.
Not only do microplastics come from larger pieces of plastic, but believe it or not, some are made *intentionally* for things like clothing, packaging, etc. A lot of the clothing that we buy that is considered fast fashion, or even some higher quality brands like nike, are made of plastic fiber derivatives such as polyester, that end up in our oceans 

>The aim of my research is to quantify the **abundance** and **types** of microplastics across deep-sea habitats, particilarly within the **Channel Islands** and **Montery Bay National Marine Sanctuaries** (NMS).I will be exploring the abundance of microplastics as a function of depth and proximity to shore, and investigating biological orgainsms for possible microplastic ingestion.


# How did I collect these deep-sea samples?

<font size="4"> Aboard the Exploration/Vessel Nautilus!</font> 

![Exploration Vessel Nautilus](https://nautiluslive.org/sites/default/files/styles/responsive_image_md/public/images/2022-03/EVNautilus%202021_MAX_0144.jpg?itok=xnnyyC1M)

- <font size="4"> In my second year of grad school, my inital project got cancelled due to Covid-19, so I was left to figure out something new. I decided to ask my outside employer if I could collect samples on their ship while I was working as a manager in training, and they said yes!!!</font> 

- <font size="4"> On this 240 foot ship, we have two Remotly Operated Vehicles (ROVs): Herculues and ARGUS that help us look around the deep-sea, collect samples, and take HD footage of every dive.</font> 



![Hercules](https://nautiluslive.org/sites/default/files/images/2021-02/NA124_JLF_7473.jpg)|  ![ARGUS](https://nautiluslive.org/sites/default/files/styles/twitter_card/public/images/2020-04/argus.jpg?itok=sVmti_6T)

- <font size="4"> The two ROV's are connected in tandem. ![tandem](https://expeditionworkshops.files.wordpress.com/2014/07/tandem-rov.jpg) 

>ARGUS is like the pendulum that absorbs wave movement, and the movement of the ship as we travel, allowing Hercules to have more fine and precise movemenets for sampling and transects.</font> 






# E/V Nautilus 2020 Expedition: NA116 & NA117
## Cruise Map: sampling locations
![sample map](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/Sample Map.png)

# Sample Collection
<font size="4"> The following sample types were collected to gain a better understanding of the density, and characterization of microplastic in the deep-sea:</font>

- <font size="4"> Water samples (niskin)</font>
- <font size="4"> Sea Urchins</font>
- <font size="4"> Sea pens</font>
- <font size="4"> Sediment</font>
- <font size="4">  Sea Pigs</font>
- <font size="4"> Drift Algae</font>




### Example plot: Let's start playing around with data viz!

```r
library(tidyverse)
library(here)

samples<-read.csv("/Users/taylorannsmith/Desktop/Smith_Final/Independent project/data/All Nautilus Samples.csv")

sample_type_scatter1 <-ggplot(data=samples, 
       mapping = aes(x = Depth..m.,
                     y = Normalized_total,
                     group = Sample_type,
                     color= Sample_type)) +
  geom_point()+ 
  geom_smooth(method = "lm")+ 
  labs(x = "Depth (m)", 
       y = "Total number of microplastics",
       title = "Total microplastics found across sample types by depth (m)"
  ) +
  scale_color_viridis_d()+
  facet_wrap(~Sample_type)+
  guides(color = "none")



sample_type_scatter1
```

<img src="Smith_Final_Project_files/figure-html/unnamed-chunk-1-1.png" width="672" />

```r
ggsave(here("Smith_Final","Independent project","output", "sample_type_scatter1.png"))#Save the plot as a png in the correct folder
```






## Water Samples

- <font size="4">  5L Niskin bottles were used to collect water from the epipelagic zone, all the way to the Abyssalpelagic Zone (0-3,800 meters deep!).</font> 


- <font size="4"> Niskins work by both ends of the bottle snapping shut when triggered, capturing water at that exact point in the water column.</font> 

![Niskin Firing](https://www.generaloceanics.com/blog/wp-content/uploads/2020/08/bottles_of_GO.jpg)


- <font size="4"> All water samples were filtered onto polycarbonate filters to colect any microplastics present the ship using a vaccum pump </font> 

![Filter](https://blog.response.restoration.noaa.gov/sites/default/files/blog-wysiwyg-images/florida-microplastic-awareness-project-filter-paper-petri-dishes_credit-university-florida_ifas_1000.jpg)



- <font size="4"> The plastics were then counted under a dissecting scope, and will be matched with confrimed plastic types via MicroFTIR Imaging </font> 

![Wagner et al. 2017](https://www.researchgate.net/profile/Jeff-Wagner-3/publication/316365358/figure/fig2/AS:621958009987072@1525297753241/Microplastic-particles-extracted-from-laboratory-medaka-GI-tracts-For-all-FTIR-spectra.png)


![Plot1](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/output/barplot.png)


# Exploring the data a bit further
I used the following packages throughout this markdown file:

```r
library(tidyverse)
library(rmdformats)
library(here)
library(hrbrthemes)
library(viridis)
library(htmlwidgets)
library(plotly)
```



Next, I attach my csv file and filter the data

```r
samples<-read.csv("/Users/taylorannsmith/Desktop/Smith_Final/Independent project/data/All Nautilus Samples.csv")
data3<- read.csv("/Users/taylorannsmith/Desktop/Thesis R/Final Niskin Data.csv")


Water_Samples <-filter(.data= samples, Sample_type== "Niskin")
Urchins<-filter(.data= samples, Sample_type== "Urchin")
Sea_pens<-filter(.data= samples, Sample_type== "Sea Pen")
Drift_algae<-filter(.data= samples, Sample_type== "Drift Algae")
Sediment<-filter(.data= samples, Sample_type== "Push Core")
Sea_pigs<-filter(.data= samples, Sample_type== "Sea Pig")


Pioneer_Canyon_North<-filter(.data = samples, Site== "Pioneer Canyon North")
Octocone_Whalle_Fall<-filter(.data = samples, Site== "Octocone/Whalle-Fall")
South_Ancapa_Slope<-filter(.data = samples, Site== "South Ancapa Slope")
Poti_Penninsula<-filter(.data = samples, Site== "Poti Penninsula")
Santa_Lucia_Palm<-filter(.data = samples, Site== "Santa Lucia Palm")
Southwest_Davidson_Seamount<-filter(.data = samples, Site== "Southwest Davidson Seamount")

Offshore_San_Miguel<-filter(.data = samples, Site== "Offshore San Miguel")
West_San_Miguel_Shelf<-filter(.data = samples, Site== "West San Miguel Shelf")
Rock_Bridge<-filter(.data = samples, Site== "Rock Bridge")
North_Santa_Cruz<-filter(.data = samples, Site== "North Santa Cruz Island")
Santa_Lucia_Escarpment<-filter(.data = samples, Site== "Santa Lucia Escarpment ")# Go back and delete space after the title in excel
```




<font size="4">Lets take a closer look at the water samples:</font>

![bubble.plot1](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/output/Bubble_plot.png)



<font size="4">Now, lets look at these samples, but grouped by the National Marine Sanctuaries</font>


<img src="Smith_Final_Project_files/figure-html/unnamed-chunk-4-1.png" width="672" />




# Current Work

<font size="4"> I am currently in the process of transferring the materials, I found and believe to be plastic, onto glass slides to be inspected using a MicroFTIR in Dr. Clare Steeles lab at CSUCI. This machine works by analyzing samples with a broad frequency spectrum of infra-red light. There are libraries loaded in the FTIR that have confirmed plastics in them from factories, and I can compare the reading of my samples to the known plastics to see what percent match I found. We will not see a 100% becasue the plastics I found have been weathered, broken down, and fouled for who knows how long</font> 

<font size="4">Here is a confirmed nylon plastic fiber I found from one of my deep-sea water samples:</font> 

![Nylon Fiber Credit: Steele Lab CSUCI](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/Nylon.jpg)




# Conclusions
- <font size="4">The highest density of microplastics seems to be found within the pelagic zone(0-200m), which makes sense, as microplastics are light in weight in comparison to water and come mostly from humans on ships and from onshore.</font>

<font size="4">Overtime however, these plastics can become fouled with organic material, causing them to sink. Another way these plastics may be finding their way into the deep-sea vie deep-sea circulation currents</font>

![Circulation](https://oceanexplorer.noaa.gov/facts/media/currents-800.jpg)


- <font size="4">There is still a lot of exploring I have to do with my data, and statistcal tests! This is just an overview of how I am begining to vizualize my data before begining analysis</font>




# Bonus Photos

<font size="4"> Here is one of the sea pigs that I collected, they are related to sea cucumbers!</font>

![Credit: “Ocean Exploration Trust and NOAA](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/seapig.png)


![Credit: “Ocean Exploration Trust and NOAA](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/herccoolview1.png)


![Credit: “Ocean Exploration Trust and NOAA fish](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/rattail.png)

![Credit: “Ocean Exploration Trust and NOAA](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/beautifulbamboo.png)

![Credit: “Ocean Exploration Trust and NOAA](/Users/taylorannsmith/Desktop/Smith_Final/Independent project/whalefallpic.png)
