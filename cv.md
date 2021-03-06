---
layout: page
title: CV
---

------

## Education

[**University of Wisconsin - Madison**](http://www.wisc.edu/) <span style="float: right;">Sept 2015 - Present</span>  
MS/PhD, [Department of Computer Sciences](http://www.cs.wisc.edu/) 


[**Indian Institute of Technology - Delhi**](http://www.iitd.ac.in/)  <span style="float: right;">July 2008 - July 2013</span>  
B.Tech. & M.Tech., [Computer Science & Engineering](http://www.cse.iitd.ac.in/)  

-----

## Work Experience

**Resarch Assistant, University of Wisconsin - Madison** <span style="float: right;">Sept 2016 - Present</span>
<br/>*WISR Group*

**Research Intern, Microsoft Research - Redmond** <span style="float: right;">June 2020 - Aug 2020</span> 

**Visiting Researcher, MIT CSAIL** <span style="float: right;">Sept 2019 - May 2020</span>

**Research Intern, Microsoft Research - Redmond** <span style="float: right;">May 2017 - Aug 2017</span>  
*Mobility and Networking Group* 

**Research Associate (Intern), Hewlett Packard Labs** <span style="float: right;">May 2016 - Aug 2016</span>  
*Networking & Mobility Group* 

**[Software Engineer (Blue Scholar)](https://www.research.ibm.com/irl/bluescholar.html)** <span style="float: right;">July 2013 - July 2015</span>    
[**IBM Research - India**](http://www.research.ibm.com/labs/india/)  
*Data Center Networking Research Team*

**Intern, American Express**  <span style="float: right;">May 2012 - July 2012</span>  
*Big Data Labs Team*

**Research Intern**, [**Avaya Labs**](http://www.avaya.com/usa/avaya-labs/)  <span style="float: right;">May 2011 - July 2011</span>  
*IP Communications Team*

-----

## Publications

K. Mahajan, A. Balasubramanian, A. Singhvi, S. Venkataraman, A. Akella, A. Phanishayee, and S. Chawla. [Themis: Fair and Efficient GPU Cluster Scheduling](http://wisr.cs.wisc.edu/papers/nsdi20-themis.pdf), *NSDI 2020*.

K. Mahajan, M. Chowdhury, A. Akella, and S. Chawla. [Dynamic Query Re-planning Using QOOP](http://wisr.cs.wisc.edu/papers/osdi18-qoop.pdf), *OSDI 2018*.

K. Mahajan, D. Sharma, and V. Mann. ATHENA: Reliable Multicast for Group
Communication in SDN-based Data Centers, *COMSNETS 2017*.

K. Mahajan, R. Poddar, M. Dhawan, and V. Mann. [Jury: Validating Controller Actions in Software-Defined Networks](http://ieeexplore.ieee.org/document/7579734), *DSN 2016*.

D. Sharma, R. Poddar, K. Mahajan, M. Dhawan, and V. Mann. [Hansel:
Diagnosing Faults in OpenStack](http://conferences2.sigcomm.org/co-next/2015/img/papers/conext15-final156.pdf), *CoNEXT 2015*.

M. Dhawan, R. Poddar, K. Mahajan, and V. Mann. [SPHINX: Detecting
Security Attacks in Software-Defined
Networks](http://www.internetsociety.org/doc/sphinx-detecting-security-attacks-software-defined-networks),
*NDSS 2015*.

K. Mahajan, D. Agarwal, and V.J. Ribeiro. [QoS aware overlay MAC layer for Coexistence of Heterogeneous Networks over Whitespaces](http://dx.doi.org/10.1109/COMSNETS.2014.6734876), *COMSNETS 2014*.

J. Buford, K. Mahajan, and V. Krishnaswamy. [Federated Enterprise and Cloud-based Collaboration services](http://dx.doi.org/10.1109/IMSAA.2011.6156338), *IMSAA 2011*.

-----

## Patents

M. Dhawan, K.S. Mahajan, R. Poddar, and V. Mann. Securing of
Software-Defined Network Controllers. US Patent 20,160,050,223. 2016.

M. Dhawan, K.S. Mahajan, R. Poddar, and V. Mann. Verifying Controller 
Actions in Software-Defind Networks with Controller Clusters. 
Filed August 2015. (IN920150132US1).

M. Dhawan, K.S. Mahajan, V. Mann, R. Poddar, and D. Sharma. Diagnosing 
Faults in Stateless Distributed Computing Platforms. Filed November 2015.
(IN920150282US1).

-----

## Projects


**Athena** <span style="float: right;">IBM Research 2015</span>  
*Keywords: Multicast, Open Source, OpenStack VM provisioning.*  

- Developed a *reliable, tcp-friendly multicast scheme* for SDN-based data
centers.
- Implementation touched upon several Open Source projects –
	- Introduced a *nak-based rate-adaptive* transport fabric in the *[openpgm](https://code.google.com/p/openpgm/)* library.
	- Implemented a reliable packet cache in the *[OpenDayLight](https://www.opendaylight.org/)* controller.
	- Modified *[OpenStack](https://www.openstack.org/) Nova & Glance* to integrate multicast for VM provisioning. Improvements of more than 2.5x achieved for typical workloads in a small data center.

**Jury**  <span style="float: right;">IBM Research 2014-15</span>  
*Keywords: Distributed Controllers, Action validations.*

- Developed an *out-of-band controller-agnostic consensus mechanism* to validate actions taken by distributed controllers.
- Evaluated against the *[ONOS](http://onosproject.org/)* & *[OpenDayLight](https://www.opendaylight.org/)* controller.

**Hansel**  <span style="float: right;">IBM Research 2015</span>  
*Keywords: OpenStack, Fault diagnosis.*  

- Proposed the construct of an *execution graph* to track network-trace based operation lineage.
- Modified the *[brocolli](https://github.com/bro/broccoli)* network monitor for realtime root-cause analysis of faults in *[OpenStack](https://www.openstack.org/)*.

**Sphinx**  <span style="float: right;">IBM Research 2013-14</span>    
*Keywords: OpenFlow, SDN, security analysis, threat detection*  

- Exposed several threat vectors in popular OpenFlow SDN controllers.
- Developed a controller-agnostic system for realtime security attack detection. Our system analysed control-plane traffic to construct incremental flow-graphs. Attack detection involved validation of invariants on the flow metadata and the graph-structure.

**Coexistence of Heterogeneous Networks over Whitespaces** <span style="float: right;">IIT Delhi 2012-13</span>  
*Keywords: TV Whitespaces, Coexistence, Layer 2 protocols*  

- Proposed a *minimal, overlay MAC layer* to solve cross-technology interference issues.
- Simulated this as a wrapper over 802.11 & 802.16 in the *[QualNet](http://web.scalable-networks.com/content/qualnet)* simulator.

**Parallel Large Scale Feature Selection** <span style="float: right;">American Express 2012</span>  
*Keywords: Hadoop, Map Reduce, Feature Selection, Logistic Regression, Big Data*  

- Implemented an *incremental forward feature selection technique* using logistic regression.
- The regression was approximated using Newton’s method to enhance the algorithm’s scale-out properties to gel well with Map Reduce framework. It was used on AmEx consumer risk datasets.

**PintOS** <span style="float: right;">IIT Delhi 2011</span>  
*Keywords: Operating Systems, PintOS*

- Implemented threads, processes, virtual memory and a file system on top of the bare bones PintOS.

**[Logisim at IITD](http://www.cse.iitd.ernet.in/~cs5080214/logisim.html)** <span style="float: right;">IIT Delhi 2009-11</span>  
*Keywords: Open Source, Simulator, Digital Logic Circuits, Architecture*  

- Extended the Open Source Java Application, Logisim, to construct and simulate digital logic circuits. The extended feature set has intelligent auto-wire routing and floating point based arithmetic.
- It is used in CSL211(Computer Architecture) as a framework to design & test student assignments.

-----

## Achievements  

Selected at [IBM Research - India](http://www.research.ibm.com/labs/india/) as part of the elite [*Blue Scholar Program*](https://www.research.ibm.com/irl/bluescholar.html) (2013-15).

Lead a team of IITD students to [*3rd place*](http://www.astronautical.org/node/177) out of 26 teams from 7 countries in the [Cansat Competition](http://www.cansatcompetition.com/Main.html) hosted by AAS, AIAA & NASA (2012).

Selected by [*IITD Class of ’89 Innovation Award*](http://www.iitdinnovationaward.org/2011-12) for being among the five most innovative projects for the project *Expressive Text-to-Speech Synthesis System for Hindi using HNM and HMM* (2012).

Awarded the *IIT Delhi Institute Merit Award* (2008-09).

Secured *All India Rank 231* in the All India Joint Entrance Examination (IIT-JEE 2008).

Stood *3rd & 4th* in Regional Mathematics Olympiad from the Maharashtra & Goa Region – judged to be the toughest region in India (2008 & 2007).

Recipient of the *National Talent Search Examination (NTSE)* Scholarship (2006-07).

-----
