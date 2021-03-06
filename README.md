#### Title:  Recomendations to contenarized your bioinformatics software


Authors: Yasset Perez-Riverol , Felipe da Veiga Leprevost, Michael R. Crusoe


## Introduction

The ability to reproduce the original results of a scientific discovery has been one of the mayor challenges
in modern science. Evidences from multiple authors suggest that reproducibility in biomedical research is lower than 85% [PMID: 24411643], while 90% of researchers agree in a reproducibility crisis [PMID: 27225100]. One of the major drawbacks is to be able to reproduce the bioinformatics analysis, including the data processing and statistical downstream analysis [PMID: 24204232]. Different authors has pointed three main premises for reproducible bioinformatics software deplyoment: (i) the use of exact versions of software and tools, (ii) open source of the code and all custom software, (iii) adopt a licence and comply with the licence of third-party dependencies [PMID: 24204232, 28751965]. Most of these works has been focussed in the openness and availability of the tools, softwares, scripts and data to perform the bioinformatics analysis [PMID: 24204232, 27415786].

However, even if source code and data are published in a public repository (e.g Github) alongside the paper as open source artifacts, they come with many dependencies, configurations, versions that make their use hard to achieve [DOI:10.1145/2723872.2723882]. The build, installation and deployment of the bioinformatics solution (e.g. software or workflow) often requires internal knowledge that is missing from the published manuscript. In addition, most of the bioinformatics software is developed by different teams but used in combination thorugth workflows, scripts or pipelines. This adds an additional layer of complexity that introduce challenges for dependency compatibilities, serial and parallel steps, varied software data file types and user-defined parameters.

Software containers has emerged as a powerful technology to documment, distribute, and deploy bioinformatics software [PMID: 28379341]. Containers are easily packaged, lightweight software components and libraries designed to run anywhere [PMID: 28379341]. Among different options Conda packages, Docker and Singularity containers are promising technologies for the field of computational biology and bioinformatics software reproducibility. The BioContainers and BioConda communities released more than 3000 containers [PMID: 28379341] for bioinformatics community enabling the development of complex and reproducbles workflows and pipeines [PMID: 28559010, PMID: 27137889].

This manuscript describes a core set of recommendations and guidelines to improve the quality and sustainability of research software based on software containers. It provides easy-to-implement recommendations that encourage adoption of containers technologies in bioinformatics and software development for research. It provides recomendations about making research software and its source code more reproducible, deployable, reusable, transparent and more compatible with other tools and software.

In this manuscript, software is broadly defined to include command line tools, graphical user interfaces, application program interfaces (APIs), infrastructure scripts and software packages (e.g. R packages).

### 1. One tool, one container.

Microservice and modular architecutres [DOI: 10.1109/MS.2016.64] is a way of breaking large software projects into smaller, independent, and loosely coupled modules. This software applications can be seen as a suite of independently deployable, small, modular components in which each tool runs a **unique** process and communicates through a well-defined, lightweight mechanism to serve a business goal [DOI: 10.4103/2153-3539.194835]. Each of these indeppendent modules are referred to as a _container_.  A container is essentially an encapsulated and immutable version of an application, coupled with the bare-minimum operating system components (e.g. dependencies) required for execution [PMID: 28379341].

Containers should be defined as mosr granulaer as possible with the premise _one Tool, one Container_. Each container should encapsulate only one piece of software, tool that perform a unique task with a weel-define goal (e.g. sequence alligner, mass spectra identification). In order to design the level of _granularity_, different metrics should be consider:

- _Lower complexity_: the encapsulated software shouldn't be a complex enviroment of dependencies, tools and scripts.
- _Reusability_: a tool condainer can be safely reused by any other workflow component or tasks through its access interface.
- _Interoperability_: different tools can be easily connected.
- _Maintainability_: the mainteiners of the software component should be take into account. If multiple tools comming from multiple teams and developers is added to the same container it makes their mantenability more complex.
- _User’s acceptability_:  tool container encapsulates domain business process units, so it can be more easily checked and used.
- _Container Size_: An important factor to define the granularity of a container is the size. Smaller containers are much quicker to download the image from registries and therefore it can be distributed to different machines much quicker. Less code/less programs in the container means less attack surface.

### 2. Keep everything minimun.

### 3. Versions should be explicit

### 4. Eschew ENTRYPOINT

### 5. More Metadata

### 6. When possible first a package and then a container.

Package managers automate the installation of complex sets of software packages. _Conda_, the most popular package manager in research software, quickly installs, runs and updates packages and their dependencies. It handles dependencies for many languages such as C, C++, R, Java and of course Python tools. In addition, _Conda_ has join to other popular packages manager systems such as Gentoo, BSD Ports, MacPorts, and Homebrew which build packages from source instead of installing from a pre-built binary.

You can create a _Conda_ package by defining a _BioConda_ recipe (**Box 1**). This recipe (https://github.com/bioconda/bioconda-recipes) contains enougth information about the dependencies, the LICENSE and fundamental metadata to find, retrieve and use the package (see **Recomendation X**). The _BioConda_ package can be use in any with any Python installation and the BioContainers project [PMID: 28379341] has developed an automatic system to build software containers for multiple technolgies such as Docker, rkt or Singularity [PMID: 28494014].
