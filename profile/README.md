## General description

**EnergyModelsX** is a multi nodal and carrier energy system modelling framework, written in Julia.
**EnergyModelsX** was developed at the Norwegian research organization [SINTEF](www.sintef.no/en) at the institutes SINTEF Energi and SINTEF Industri.
The model is based on the [`JuMP`](https://jump.dev/JuMP.jl/stable/) optimization framework.
It is a multi-carrier energy model, where the definitions of the resources (both energy and material) and the technologies are fully up to the user of the model.
One of the primary design goals was to develop a framework that can easily be extended with new functionality without the need to understand and remember every variable and constraint in the model.
In addition, extending the framework should not require any changes to the core structure of the framework, simplifying its application in specific case studies.
To this end, the model is developed in multiple individual packages that can be extended to include, *e.g.*, improved technology descriptions, specific required technology nodes, or new resources with different properties.

## Available packages

### Core packages

The following packages are core packages and are required for setting up a model using the EnergyModelsX framework.

#### TimeStruct.jl

TimeStruct is a package providing functionality for different time structures in the framework. A created model can utilize both a single-level and two-level time structure depending on the chosen time structure approach.
TimeStruct allows furthermore for both operational and strategic scenarios.
This feature is however not yet implemented in the EnergyModelsX framework.

#### EnergyModelsBase.jl

EnergyModelsBase is the core structure of the EnergyModelsX framework.
It can be used to design an operational model without inclusion of geographical features.
In this respect, it can be seen as a regional energy modelling framework.
It includes reference technologies/nodes for energy/material sources, conversion technologies, storage technologies, and sinks.
The individual nodes can be either connected through a common availability node that satisfies the energy/mass balance at each individual operational time period or through direct coupling between the individual technology nodes.
Extensions of EnergyModelsBase can be achieved through dispatching on several abstract types.

One aim of EnergyModelsBase is to avoid string comparisons within the code. Instead, it uses exclusively the developed abstract and composite types for model creation.

### Extension packages

Extension packages do not have to be included within a model.
They offer however additional functionality to the core structure.
Depending on the requirements of the developed model, it is possible to add, *e.g.*, a concept of geography or investments to a chosen model.
The list of included extension packages will be updated based on future releases.

#### EnergyModelsGeography.jl

EnergyModelsGeography extends the base package for inclusion of energy and mass transmission between different areas.
Each area can consist of different technology nodes.
In that respect, EnergyModelsX allows for specifying explicitly which technologies are allowed in the individual areas, while other frameworks enforce that through parameters setting the maximum capacity to 0.
Transmission between areas can also be differentiated in different transmission modes.
This allows to distinguish between, *e.g.*, power lines and pipelines.

#### EnergyModelsInvestments.jl

EnergyModelsInvestments adds investment options for the individual technology nodes.
In addition, each technology node can have a different investment option, like discrete, semi-continuous, or continuous investments.
EnergyModelsInvestments utilizes a weak dependency for geographical investments.

## Disclaimer

The individual packages of **EnergyModelsX** are under constant development.
Hence, breaking changes can occur, although we aim at maintaining backwards compatibility for developed models through the application of constructors.

## Acknowledgement

The development of **EnergyModelsX** has been funded by the Norwegian Research Council in the project [Clean Export](https://www.sintef.no/en/projects/2020/cleanexport/), project number [308811](https://prosjektbanken.forskningsradet.no/project/FORISS/308811).
The authors gratefully acknowledge the financial support from the user partners Å Energi, Air Liquide, Equinor Energy, Gassco, and Total E&P Norge.
