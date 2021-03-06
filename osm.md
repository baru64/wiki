<!-- TITLE: The 5GinFIRE MANO platform -->
<!-- SUBTITLE: A description of the 5GinFIRE MANO platform -->

# The 5GinFIRE MANO platform
The 5GinFIRE MANO platform is the system that enables the management and orchestration of network services (NS), potentially composed of multiple VxFs, across the NFV experimental infrastructures provided by 5GinFIRE partners. To fulfill this objective, the platform offers a northbound interface to the 5GinFIRE portal, enabling the operations that are needed to support the execution of experiments (e.g., onboarding a NS and a VxF). A simplified overview of the 5GinFIRE MANO platform is depicted in the figure below.

![Mano Platformv 2](/uploads/mano-platformv-2.png "Mano Platformv 2")

The platform is based on the ETSI-hosted [Open Source MANO (OSM) project](https://osm.etsi.org/), which has been adopted by 5GinFIRE to provide the functionalities of a NFV orchestrator, supporting the management and coordination of computing, storage and network resources at the diverse experimental infrastructures, as well as the lifecycle management of network services. With this purpose, the OSM stack interacts with the Virtualized Infrastructure Managers (VIM) deployed by 5GinFIRE partners. There are currently three sites deploying the components and functionalities required to operate the 5GinFIRE MANO platform, each providing an NFV experimental infrastructure: (a) an infrastructure at the global 5G Telefonica Open Innovation Laboratory (5TONIC) [2], made available by TID (founding member of 5TONIC) and UC3M (member of 5TONIC); (b) an infrastructure located at ITAv; and (c) an infrastructure made available through a collaborative agreement by UNIVBRIS and BIO. Additionally, there is an experimental infrastructure under development at UFU.

The first stable version of the 5GinFIRE MANO platform is based on OSM Release TWO, being the OSM stack hosted at 5TONIC (the team is currently working on the migration to OSM Release THREE). Inter-site communications among 5GinFIRE sites are enabled by an overlay network architecture based on VPNs (to simplify operations, the primary VPN server is hosted at the same site as the MANO stack, i.e. 5TONIC). This overlay network provides authorized partners a secure access with certificate-based authentication to 5TONIC, enabling the establishment of the following types of data exchanges: (a) communications between the OSM stack and the VIMs; (b) communications between the OSM stack and the VxFs, to support their configuration; (c) inter-site data communications among VxFs. 

The technical solution adopted by 5GinIFIRE also supports the flexible incorporation of other sites (e.g., coming from the Open Call process of 5GinFIRE), as long as they support a compliant VIM[^1] and they set up the appropriate VPN based inter-site connection mechanisms (see the information below).

[^1]: OSM Release TWO supports multiple VIMs through a plugin model, including OpenVIM, OpenStack, VMWare vCloud Director and Amazon Web Services Elastic Compute Cloud.

## Summary of NFV components and infrastructure
In the following, we summarize the main NFV components and infrastructures that have been made available for the 1st Open Call for experimentation by 5GinFIRE testbed providers. 

### 5TONIC

**NFVO**: based on OSM Release TWO (running in a virtual machine using a server computer with 16 cores, 128 GB RAM, 2 TB NLSAS hard drive and a network card with 4 GbE ports and DPDK support).

**VIM**: two instances of OpenStack Ocata, each controlling a separate NFVI (hereafter referred to as 5GinFIRE NFVI and IMDEA NFVI). 
- The first one runs in virtual machine over a server computer (6 cores, 32GB of memory, 2TB NLSAS and a network card with four GbE ports and DPDK support).
- The second one runs as a virtual machine in the same server computer as the OSM stack. 

**5GinFIRE NFVI**: 
- 3x server computers (each with 6 cores, 32GB of memory, 2TB NLSAS and a network card with four GbE ports and DPDK support)
- Interconnected by a GbE data-plane switch.

**IMDEA NFVI**:
- 2x high-profile servers (each equipped with 8 cores in a NUMA architecture, 128GB RDIMM RAM, 4TB SAS and 8 10Gbps Ethernet optical transceivers with SR-IOV capabilities).
- Interconnected by a 24-port 10Gbps Ethernet switch.

Both NFVIs are available for experimentation under the terms and conditions specified [here](https://5ginfire.eu/5tonic/).

### ITAv
**VIM**: based on OpenStack Ocata.

**NFVI**:
- 1x server computer: 24 cores, 192GB memory, 4 x 1Gbps interfaces (passthrough, DPDK and SR-IOV), 2 x 1TB SAS3 hard drives. 
- 1x server computer: 16 cores, 256 GB memory, 4 x 1Gbps interfaces (passthrough), 2 x 1TB SAS2 hard drives. 
- 1x 24-port 1Gbps switch, interconnecting the infrastructure.

### UNIVBRIS & BIO

**VIM**: based on OpenStack Ocata.

**NFVI**:
-	1x server computer: 2x8 core 16 threads CPU 2.4 GHz, 32GB RAM, Dual RAID 1 900 GB HDs.
-	1x server computer: 2x8 core 16 threads CPU 2.4 GHz, 16GB RAM, 900 GB storage.
-	1x MVB NEC optical switch, 1x ENS NEC optical switch.

## Addressing plan
Enabling effective network communications among multiple sites has required a careful definition of the IP address space to be used by interconnecting entities. In this respect, the following agreements have been taken by 5GinFIRE:

1)	Entities connecting to the 5GinFIRE MANO platform will use the private address space **10.154.0.0/16** for control and data plane communications.
2)	5TONIC will use the private address space **10.4.0.0/16** to support control and data plane communications.

The 5GinFIRE network operations center will be in charge of the allocation of IP address ranges to entities within the address space 10.154.0.0/16. The current allocation of IP addresses to sites is summarized as follows:

- **5TONIC**: 10.4.0.0/16.
- **ITAv**:	10.154.0.0/20.
- **UNIVBRIS & BIO**:	10.154.16.0/20.
- **Reserved for administrative purposes:** 10.154.255.0/23

Any potential issues related with the allocation of IP addresses to external sites that connect to the MANO platform will be treated on a case-by-case basis.

## Requirements to support the interconnection of external sites
Beyond any particular requirements that may be identified when facing the interconnection of specific external sites, which will be treated on a case-by-case basis, in the following we indicate a non-exhaustive list of requirements that must be fulfilled by external entities to connect to the 5GinFIRE MANO platform:

1) Utilization of a compliant VIM solution, i.e., compliant with OSM Release TWO[^2].
2) Obtaining an appropriate IP address space, along with VPN credentials to gain a secure access to 5TONIC, from the 5GinFIRE network operations center. 
3) Configuration of the site with the allocated IP address space.
4) Configuration of any necessary VPN endpoints, to connect the site to the overlay network of the 5GinFIRE MANO platform. These endpoints will then support the exchange of control and data-plane information with the other NFV components of 5GinFIRE (OSM stack, VxFs, etc.).
5) Configuration of the appropriate VIM networks to enable control and data-plane communications with the VxFs deployed at the entity’s datacenter,
and using the allocated IP address space.
6) Support routing of control and data plane information across the local network segments of the external entity, to support communications between the VPN endpoints and the VIMs/VxFs and vice versa.

