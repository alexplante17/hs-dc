# Hyper Scaler DC
There are plenty of technical challenges associated with the build of the hyper-scalre infrastructure, which exists behind some biggest infrastructures hosting cloud platforms. This repo makes attempt to recreate at high-level the design of such a data centre.

## Used platforms
### Data Centre
- Mellanox P4-switch
- Microsoft Azure SONiC

### Development host
- Linux: CentOS 7
- Containers: Docker 19.03.8
- Automation and orchestartion: Python 3.8
- Graph modelling: NetworkX 2.4
- Visualisation: Graphviz 2.30.1

## Structure
Main components:
- The `topology` directory contains the files with the samle of the of physical and logical topology of the micro pod.
- The `infrastructure` directory contains the directors with the files of the switches running Microsot Azure SONiC

## To-do list
The following ideas are in the pipeline to be implmeneted:
- Automated rollout and provisioning of the network based on graph topology and YAML descriptors
- High-scale fabric with DC aggregarion spine
- Mutiple vendors leafs (Arista EOS, Cumulus Linux, Cisco Nexus) and interop
- Monitoring (tbd)

## Change log
Relesase `0.1.1`:
- Added the `inventory` folder containing the information for the topology generation.
- The intend topology is stored in `inventory/build.yaml`.
- The Bash script `prepare.sh` installs the Graphviz software from the original repository. The version for CentOS is used, so may requre changes if you use another operation system.
- The visualisation of the topology is done using the `pydot` and `graphviz` modules for Python. The autogenerated topology is stored in `topology` folder in both `dot` and `png` formats.

Release `0.1.2`:
- Changing the colouring of the nodes.
- Changed the pod structure per the blogpost (HS. Part 2.).

Release `0.1.3`:
- Modifying the colouring so that each pod and each aggs have their own colours.

Release `0.2.0`:
- The generation of a network graph is taken from the Graphviz module to NetworkX as it allows to do math operations on graph.
- The Graphviz is used only for visualisation of the graph, not for its build.
- The content of the `requirements.txt` is changed.
- The original `main.py` is moved to `backup` folder and is named now `main013.py`. Same is done for `requirements.txt`.
- The Bash script `prepare.sh` also installs the `graphviz-devel` package necessary for Python's `pygraphviz` to work.

Release `0.2.1`:
- Added `resource.yaml` file in `inventory` directory. It contains some logical resources (BGP ASN, IP addresses), which are used in the topolgy graph build.
- Added the attribute `bgp_asn` to the node containing the switches. It is automaticaly calculated to be unique per each network device.
- Interfaces are created as nodes. So now the grap view is changed. The full link between devices looks like as `dev_a -- port -- port -- dev_b`.

## Additional resources
- NetworkX: https://networkx.github.io
- Graphviz: http://graphviz.org

# Do you want to automate network like a profi?
Join the network automation course: http://training.karneliuk.com

(c) 2016-2020 karneliuk.com

