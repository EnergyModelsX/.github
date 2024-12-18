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

#### [TimeStruct.jl](https://sintefore.github.io/TimeStruct.jl/stable/)

TimeStruct is a package providing functionality for different time structures in the framework. A created model can utilize both a single-level and two-level time structure depending on the chosen time structure approach.
TimeStruct allows furthermore for both operational and strategic scenarios.
This feature is however not yet implemented in the EnergyModelsX framework.

#### [EnergyModelsBase.jl](https://github.com/EnergyModelsX/EnergyModelsBase.jl)

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

#### [EnergyModelsGeography.jl](https://github.com/EnergyModelsX/EnergyModelsGeography.jl)

EnergyModelsGeography extends the base package for inclusion of energy and mass transmission between different areas.
Each area can consist of different technology nodes.
In that respect, EnergyModelsX allows for specifying explicitly which technologies are allowed in the individual areas, while other frameworks enforce that through parameters setting the maximum capacity to 0.
Transmission between areas can also be differentiated in different transmission modes.
This allows to distinguish between, *e.g.*, power lines and pipelines.

#### [EnergyModelsInvestments.jl](https://github.com/EnergyModelsX/EnergyModelsInvestments.jl)

EnergyModelsInvestments adds investment options for the individual technology nodes.
In addition, each technology node can have a different investment option, like discrete, semi-continuous, or continuous investments.
EnergyModelsInvestments utilizes a weak dependency for geographical investments.

#### [EnergyModelsRenewableProducers.jl](https://github.com/EnergyModelsX/EnergyModelsRenewableProducers.jl)

EnergyModelsRenewableProducers introduces several new technology descriptions for renewable power generation technologies.
The first node type can be used for representing non-dispatchable renewable energy sources like wind or solar PV power.
Two node types correspond to two simplified implementations of hydro power, a regulated hydropower plant and a pumped hydro storage unit.
Detailed hydro power is furthermore implemented *via* several additional nodes modelling waterways and non-linear power-flow relationships.

#### [EnergyModelsCO2.jl](https://github.com/EnergyModelsX/EnergyModelsCO2.jl)

EnergyModelsCO2 introduces four new technology descriptions for technologies within the CO₂ capture and storage value chain.
The first node type is a CO₂ source as the reference source does not allow for CO₂ as output.
The second node type is a CO₂ storage node in which the CO₂ accumulates over the individual strategic periods.
The third and forth node type represent an approach for retrofitting CO₂ capture to an existing process.
It is required if you want to model investments in only the CO₂ capture unit.

#### [EnergyModelsHydrogen.jl](https://github.com/EnergyModelsX/EnergyModelsHydrogen.jl)

EnergyModelsHydrogen introduces sevel new technology descriptions for hydrogen technologies.
The first two node types are modelling electrolysis with stack replacment (both) and stack degradation (only one).
One node implements natural gas reforming with the potential for start-up, shutdown, and offline times and costs.
Two nodes implement hydrogen storage, one simplified, the other more detailed in which the compression requirement is depending on the storage level.

#### [EnergyModelsHeat.jl](https://github.com/EnergyModelsX/EnergyModelsHeat.jl)

EnergyModelsHeat provides new technologies for modelling district heating.
The key concepts are based on a new introduced resource, `ResourceHeat`, which includes temperature profiles in given regions.
Based on the resource, the package provides description for a district heating pipe with capacity and loss, a heat pump, a thermal energy storage, and a heat-exchanger that can be utilized to identify the potential energy recovery from a surplus stream.
It also includes a C++ model of a biomass combined heat and power plant which will be incorporated into an EMX node in a latter stage.

#### [EnergyModelsGUI.jl](https://github.com/EnergyModelsX/EnergyModelsGUI.jl)

EnergyModelsGUI provides a graphical user interface (GUI) for a fast visualization of both the graph of the energy system and the results of an analysis.
The visualization of the graph is based on the provided `case` dictionary, and hence, independent of whether the model is solved or not.
Model results can be visualized based on the `JuMP.model`.
It is planned in a latter stage to allow the visualization of results from saved .csv files.

## Disclaimer

The individual packages of **EnergyModelsX** are under constant development.
Hence, breaking changes can occur, although we aim at maintaining backwards compatibility for developed models through the application of constructors.

## Cite

If you find `EnergyModelsX` useful in your work, we kindly request that you cite the following [publication](https://doi.org/10.21105/joss.06619):

```bibtex
@article{hellemo2024energymodelsx,
  title={EnergyModelsX: Flexible Energy Systems Modelling with Multiple Dispatch},
  author={Hellemo, Lars and B{\o}dal, Espen Flo and Holm, Sigmund Eggen and Pinel, Dimitri and Straus, Julian},
  journal={Journal of Open Source Software},
  volume={9},
  number={97},
  pages={6619},
  year={2024}
}
```

For earlier work, see our [paper in Applied Energy](https://www.sciencedirect.com/science/article/pii/S0306261923018482):

```bibtex
@article{boedal_2024,
  title = {Hydrogen for harvesting the potential of offshore wind: A {N}orth {S}ea case study},
  journal = {Applied Energy},
  volume = {357},
  pages = {122484},
  year = {2024},
  issn = {0306-2619},
  doi = {https://doi.org/10.1016/j.apenergy.2023.122484},
  url = {https://www.sciencedirect.com/science/article/pii/S0306261923018482},
  author = {Espen Flo B{\o}dal and Sigmund Eggen Holm and Avinash Subramanian and Goran Durakovic and Dimitri Pinel and Lars Hellemo and Miguel Mu{\~n}oz Ortiz and Brage Rugstad Knudsen and Julian Straus}
}
```

## Acknowledgement

The development of **EnergyModelsX** has been funded by the Norwegian Research Council in the project [Clean Export](https://www.sintef.no/en/projects/2020/cleanexport/), project number [308811](https://prosjektbanken.forskningsradet.no/project/FORISS/308811).
The authors gratefully acknowledge the financial support from the user partners Å Energi, Air Liquide, Equinor Energy, Gassco, and Total OneTech.

The development of **EnergyModelsGUI** has been funded by the European Union’s Horizon Europe research and innovation programme in the project [Flex4Fact](https://flex4fact.eu/home-3/) under grant agreement [101058657](https://doi.org/10.3030/101058657).

The development of **EnergyModelsHydrogen** has been funded in addition to [Clean Export](https://www.sintef.no/en/projects/2020/cleanexport/) by the European Union’s Horizon Europe research and innovation programme in the project [iDesignRES](https://idesignres.eu/) under grant agreement [101095849](https://doi.org/10.3030/101095849).

The development of **EnergyModelsHeat** was funded by the Norwegian Research Council in the project [ZEESA](https://www.sintef.no/en/projects/2023/zeesa-zero-emission-energy-systems-for-the-arctic/), project number [336342](https://prosjektbanken.forskningsradet.no/project/FORISS/336342), as well as the European Union’s Horizon Europe research and innovation programme in the project [iDesignRES](https://idesignres.eu/) under grant agreement [101095849](https://doi.org/10.3030/101095849).
