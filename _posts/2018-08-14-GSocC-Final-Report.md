---
layout: post
title:  "GSoC 2018 Final Report"
date:   2018-08-14 08:28:15 +0530
categories: [FOSS,python]
image: GSOC.png
---
# Google Summer of Code 2018 : Create Environmental Science Libraries in Python using the Workflow Paradigm for HPC

### Organization name :- Earth Sciences Information Partners - National Oceanic & Atmospheric Administration

### *Mentors :-* Ryan Berkheimer(GST at NOAA NCEI) , Max Banas (DMME, Virginia)

- The link for the project proposal is here :-[Project](https://summerofcode.withgoogle.com/projects/#6467997246423040), [Proposal](https://docs.google.com/document/d/16J5oVnHwpkQzmASGKjDtQffLUg6GF92f7oPlu2AgQ1U/edit?usp=sharing) 

- This project was featured in the annual summer meeting of Earth Sciences Information Partners in a talk held on July 19, 2018. 

   
- link to the talk :- [Talk](https://meetings.esipfed.org/event/EzLj/esip-lab-incubator-outcomes-google-summer-of-code-update-advances-in-provenance-usgs-esip-lab-partnership)



- The code has been pushed in ESIP-envlib branch of ephemeral :- [Branch](https://bitbucket.org/QuantumOrigin/ephemeral/branch/Esip-envlib) 

### About ESIP :-

- ESIP has been supporting innovation and nurturing software development revolving around the Earth Sciences Domain.
- It is supported by NASA, NOAA, USGS and 110+ other member organizations.

### Goal

- Port MPI-based algorithms which have been natively implemented in C++ into pure python distributed workflow based code.
- This would lead to the library being integrated into Ephemeral, which is a scientific workflow coded by my mentor Ryan Berkheimer.
- This would in turn lay the foundation for porting of other environmental science libraries related to climate, weather, hydrology and other domains which are relatively less explored using python and/or are relying on native C++ libraries for heavy computational lifting.

### Motivation

We identified the problem of watershed delineation, which is a very common problem in Hydrology but has several subsequent applications, some of them being flood prediction, soil erosion and hydrological modeling.
[![Overview](https://i.imgur.com/ou1UhG6.png)](https://i.imgur.com/ou1UhG6.png)



 


### Progress

- Researched available algorithms for Watershed delineation and identified D8 to be the primary focus for implementation as well as outlined the various stages in delineating an end-to-end watershed. 
- Compared SRTM and ASTER DEM datasets based on their resolution and suitability
- Began implementation of flood-fill algorithm and getting acquainted with processing satellite imagery. This would act as a baseline code for subsequent implementation. [commit](https://bitbucket.org/QuantumOrigin/ephemeral/commits/e606968f0806ecfc02c6a88044c64915c4e9e3bd?at=Esip-envlib) 
- Researched different workflow engines and mainly studied about luigi which builds complex pipelines of batch jobs, similar to ephemeral in that regard. This helped identify features which can be later integrated to ephemeral
[trello board a](https://trello.com/c/6NP3OrcS/19-implement-serial-prepare-dem-job),[trello board b](https://trello.com/c/f0eSvXVv/9-complete-first-review-period-deliverables-as-specified-by-the-description-inside-this-task),[trello board c](https://trello.com/c/lvGS51Kd/10-review-flow-acc-paper-and-algorithm-and-code)[commit](https://bitbucket.org/QuantumOrigin/ephemeral/commits/4accc16a02318908cee533ca844679db5a4cb163?at=Esip-envlib)
- Serial implementation of flow direction and accumulation on a numpy array 
[commit a](https://bitbucket.org/QuantumOrigin/ephemeral/commits/c5123b4617833aa6b6af28273ce58f9c20af1ea9),[commit b](https://bitbucket.org/QuantumOrigin/ephemeral/commits/5585b64161eb71d775eb5c54c1489ecfb34e116d)
- Narrowed down the various stages and identified the flow accumulation stage. also  identified a dataset with flow direction calculated. This would help in calculating flow accumulation since it’s an intermediate step. 
[Source](https://hydrosheds.cr.usgs.gov/datadownload.php?reqdata=15dirg) 
- Performed functional decomposition on the problem which significantly helped in porting the code subsequently. This made it easier for me to code a serial implementation of the translated code quickly
[commit a](https://bitbucket.org/QuantumOrigin/ephemeral/commits/17ef7db63305f16e42536e25e2d5e68d25d009a0?at=Esip-envlib),[commit b](https://bitbucket.org/QuantumOrigin/ephemeral/commits/153bb83e0ec8689cb7486f719ef8c14d3022a7c4?at=Esip-envlib),[commit c](https://bitbucket.org/QuantumOrigin/ephemeral/commits/e0bf90c977d45530b6b98c671dbc60faee55b702?at=Esip-envlib),[commit d](https://bitbucket.org/QuantumOrigin/ephemeral/commits/7c872c8ac2d813896b520bb61ff2e24f389c35c1?at=Esip-envlib),[commit e](https://bitbucket.org/QuantumOrigin/ephemeral/commits/f6ea4d30e5e74f5333823f88c876efa63a31b8d4?at=Esip-envlib)


- Began translating code of the library which had native C++/MPI implementation of Flow accumulation, ended up translating around 1500+ lines of code 
[trello board](https://trello.com/c/BbcNxMff/26-implement-parallel-flow-accumulation-job),[commit a](https://bitbucket.org/QuantumOrigin/ephemeral/commits/295c082c3d2111a562454cc766d6ffe5c02bb52c),[commit b](https://bitbucket.org/QuantumOrigin/ephemeral/commits/1c7ef4304cfe0183b6ff4a824437fccefad77c91),[commit c](https://bitbucket.org/QuantumOrigin/ephemeral/commits/965e315a0555c3115051a98935e88151069aaa91),[commit d](https://bitbucket.org/QuantumOrigin/ephemeral/commits/295c082c3d2111a562454cc766d6ffe5c02bb52c)[commit e](https://bitbucket.org/QuantumOrigin/ephemeral/commits/d43b96af3a2ea1d8c1db62ea2347d1ca12872648)
- Implemented a serial version of the code and tested it on 15 sec GRID flow direction datasets [commit a](https://bitbucket.org/QuantumOrigin/ephemeral/commits/31e2aa7c75c71c76b103c0a07e70efa87059cf8e)

>Input of a sample flowdirection grid :- 
[![Input](https://i.imgur.com/Nlo2zfE.png)](https://i.imgur.com/Nlo2zfE.png)

>Corresponding flow accumulation output as a netCDF raster:- 
[![Output](https://i.imgur.com/HXPZHQj.png)](https://i.imgur.com/HXPZHQj.png)




### COMMITS

| Sr.No | Linked Commit |Description|
| ------ | - | ------ |
| 1 | [c5123b4](https://bitbucket.org/QuantumOrigin/ephemeral/commits/c5123b4617833aa6b6af28273ce58f9c20af1ea9?at=Esip-envlib) |Serial code, flow direction done, debug flow accumulation |
| 2 | [5585b64](https://bitbucket.org/QuantumOrigin/ephemeral/commits/5585b64161eb71d775eb5c54c1489ecfb34e116d?at=Esip-envlib) |fixed flow accumulation. |
| 3 | [934f590](https://bitbucket.org/QuantumOrigin/ephemeral/commits/934f5909b271b0c2ad2047d1e13a5f306dd8e63b?at=Esip-envlib) |begin parallel flow accumulation from C++ implementation |
| 4 | [1c7ef43](https://bitbucket.org/QuantumOrigin/ephemeral/commits/1c7ef4304cfe0183b6ff4a824437fccefad77c91?at=Esip-envlib) |some classes translated |
| 5 | [965e315](https://bitbucket.org/QuantumOrigin/ephemeral/commits/965e315a0555c3115051a98935e88151069aaa91?at=Esip-envlib) |port v1.2|
| 6 | [0460be3](https://bitbucket.org/QuantumOrigin/ephemeral/commits/0460be3cd9eaea23bc576d81c86965ca86057ad1?at=Esip-envlib) |file rename, no spaces |
| 7 | [295c082](https://bitbucket.org/QuantumOrigin/ephemeral/commits/295c082c3d2111a562454cc766d6ffe5c02bb52c?at=Esip-envlib) |all translation done, cleanup pending |
| 8 | [d43b96a](https://bitbucket.org/QuantumOrigin/ephemeral/commits/d43b96af3a2ea1d8c1db62ea2347d1ca12872648?at=Esip-envlib) |re-commit |
| 9 | [31e2aa7](https://bitbucket.org/QuantumOrigin/ephemeral/commits/31e2aa7c75c71c76b103c0a07e70efa87059cf8e?at=Esip-envlib) |serial flow accumulation - netCDF |
| 10 | [4accc16](https://bitbucket.org/QuantumOrigin/ephemeral/commits/4accc16a02318908cee533ca844679db5a4cb163?at=Esip-envlib) |added luigi program for printing numbers in one file and their squares or cubes in another file and with instructions on how to run it|
| 11 | [f6ea4d3](https://bitbucket.org/QuantumOrigin/ephemeral/commits/f6ea4d30e5e74f5333823f88c876efa63a31b8d4?at=Esip-envlib) |Added a json file of a sample job within a workflow |
| 12 | [7c872c8](https://bitbucket.org/QuantumOrigin/ephemeral/commits/7c872c8ac2d813896b520bb61ff2e24f389c35c1?at=Esip-envlib) |Added a sample task json within ephemeral workflow|
| 13 | [e0bf90c](https://bitbucket.org/QuantumOrigin/ephemeral/commits/e0bf90c977d45530b6b98c671dbc60faee55b702?at=Esip-envlib) |Added a specification example for ephemeral workflow |
| 14 | [153bb83](https://bitbucket.org/QuantumOrigin/ephemeral/commits/153bb83e0ec8689cb7486f719ef8c14d3022a7c4?at=Esip-envlib) |List of tasks json file added |
| 15 | [17ef7db](https://bitbucket.org/QuantumOrigin/ephemeral/commits/17ef7db63305f16e42536e25e2d5e68d25d009a0?at=Esip-envlib) |created list-of-tasks.json(partial) |
| 16 | [e606968](https://bitbucket.org/QuantumOrigin/ephemeral/commits/e606968f0806ecfc02c6a88044c64915c4e9e3bd?at=Esip-envlib) |flood fill implementation |

##### 9882 lines of code added. [source for commit and diff history](https://bitbucket.org/QuantumOrigin/ephemeral/branch/Esip-envlib#commits)  


### TODO
[Link to my proposal](https://docs.google.com/document/d/16J5oVnHwpkQzmASGKjDtQffLUg6GF92f7oPlu2AgQ1U/edit?usp=sharing)
I feel that we have achieved most of what we set out to do in terms of deliverables, for the tough part is done in implementing the various phases through code. It is comparatively straightforward to replicate the code for the part that is still left. Since this was a research-oriented project i can fondly look back to find that it's been an enriching experience for me in terms of learning as well as contributing.
- The Translated code won’t work directly. Work on creating python wrappers for the libraries in richdem repository so that it would work. 
- Once the Code is working, make it work with dask and xarray 
Ingest it as a library in ephemeral 
- Duplicate the code for other stages of watershed delineation such as DEM sink filling and flow direction calculation
- Make it data oriented by minimizing the commands to be given by the user by creating a standard instruction format to be provided for executing once all the stages are coded
- Benchmark the code on a cluster and compare the runtime with C++ richdem implementation 
- Carry forward the work and try to have it published as a white paper
- Update the report linking to the NCEI/NESDIS publication on Hollings scholars and other young science interns where this project will be featured


### Lessons learned

GSoC has been an enriching professional experience for me! Here I list some of the takeaways and lessons learned while working and through feedback provided by my mentors:- 

- Gained a better understanding of implementing distributed workflow systems
- Functional approach to breaking down a problem. Having built code from small modules, parallelism can be leveraged 
- Working on a large scale project which additionally is a real-world problem.  
- The benefits of routine code submission which leads to targeted feedback and inputs from mentors 
- Asking  for assistance more frequently. I initially tried to solve any roadblocks by myself but it ended up slowing me down. Having a habit of figuring everything out by myself, this was a tough lesson to integrate but I reaped the benefits of it in the later stages with my mentors providing me helpful pointers when required. 
- Learning how to read code written by others. 
- Significant enhancement in python and C++ vocabulary







### Acknowledgements and final words


I am extremely grateful to my mentors  Ryan and Max for helping me out at various stages throughout the summer.  Special thanks to Annie Burgess who is the ESIP Lab Director, for facilitating the Summer Program.  

Working with ESIP under Google Summer of Code has been an amazing experience.
As a GIS Grad student, there was a lot to learn at the beginning, but persisting with the problem statement and spending more time with the libraries made things easier.
Being a student of the Earth Sciences domain, I realize the importance of this project and hence I am committed to contributing to it as much as I can ! 

The most challenging aspect of this project was probably the lack of similar efforts put into porting native parallel algorithms into pure python code and I hope that this will help others.




