.. _topics-index:

======================================================
The KIT Data Manager Repository Platform Documentation
======================================================

This documentation describes the single components of the KIT Data Manager
Research Data Repository Platform. KIT Data Manager (KIT DM) is a domain-agnostic
platform for building up research data repositories for managing research
data according to the FAIR principles. Therefor, globally agreed recommendations 
and standards, e.g. outcomes of the Research Data Alliance, are implemented and 
integrated into the platform. Due to the different requirements for a domain-agnostic
platform, all components are designed as independent as possible from each other. This 
allows to use only components required by a particular use case. This reduced complexity 
and offers a high level of flexibility for current and future challenges in the field of 
research data management.

============================
Collection API (Version 1.0)
============================

***************************************
Authors: Sabrine Chelbi, Thomas Jejkal
***************************************

The Collection API is proposed by the RDA Recommendation on Research Data
Collections doi: `10.15497/RDA00022`_. It can be used for building collections of digital
objects independent from any repository in order to facilitate data interoperability,
reuse and make collections actionable to be able to cope with ever increasing
amounts and volumes of data. 

.. _10.15497/RDA00022: http://doi.org/10.15497/RDA00022


.. toctree::
   :caption: Collection API
   :hidden:
   :maxdepth: 2

   collection/intro
   collection/installation
   collection/implementation
   collection/quickstart


:doc:`collection/intro`
    A short overview of the Collection API.
:doc:`collection/installation`
    Installation instructions.
:doc:`collection/implementation`
    illustration of the service architecture.
:doc:`collection/quickstart`
    Steps towards realizing an example use case.
    
.. note:: This documentation is not complete, yet. Build it.
