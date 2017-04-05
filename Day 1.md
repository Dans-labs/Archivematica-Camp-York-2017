Day 1
=====

Archivematica for Absolute Beginners
------------------------------------

### Slides
* [Opening and Archivematica introduction](slides/Opening%20slides%20and%20Archivematica%20introduction.pdf)
* [Archivematica - why what who how](slides/Archivematica%20-%20why%20what%20who%20how.pdf)
* [Intro to AtoM](slides/Intro%20to%20AtoM.pdf)

### History of the project
* early 2000 started, not many tools around
* 2005 AtoM - library system
* 2009 archiving/preservation/repository backend
* funding from a.o. UNESCO
* 2014 first production distribution
* main users: libraries/universities, couple government/museums
* open source project on [GitHub](https://github.com/artefactual/archivematica)
* new features by request from organizations
* about 2 releases per year
* new features in latest release:
    * fuul AIP re-ingest
    * appraisal tab
    * integration with ArchivesSpace

### University of Edinburgh - end user
* look at DPC Procuring Digital preservation event in edinburgh (Marc Fresko presentation (Infosight))
* few funding
* many options considered
* chosen Archivematica because...
    * free
    * no license
    * open source
    * uses open source microservice tools
    * takes advantage of technological development in the sector (VeraPDF, MediaConch)
    * sustainable
    * strong support in HE sector
    * integration with ArchivesSpace
    * standards align
* challenges/opportunities
    * installation - Ubuntu vs CentOS (both supported now)
    * Dspace integration
    * ArchiveSpace integration
    * Collaboration and community

### OAIS
* producer creates SIP
* send to ingest procedure
* preservation planning - looking at formats and thinking if it is good for long-term preservation
* goes on to Data management and Archival Storage (AIP) - used for long-term storage
* Archivematica doesn't store packages, it only creates them!
* making it accessible using a DIP (dissemminiation information package) for customers/consumers

### Archivematica general overview
* 1-1 mapping from OAIS to Archivematica UI
* microservice architecture and job structure within microservice
* standards: BagIt, METS (metadata encoding), PREMIS (preservation metadata), Dublin Core (descriptive metadata), PRONOM
* many external tool usage
* various storage offers, hosting, local, cloud (amazone, microsoft)
* providing access using atom, archivesspace, dspace

### Archivematica demo
* transfer dashboard - do most of the work
* multiple transfers (creating SIP):
    * standard - just a folder of documents/images/etc.
    * zipped bag - bagit style in zip
    * unzipped bag - bagit style
    * dspace - exporting dspace AIP and preserve it here
    * disk images
* METS.xml encodes all metadata (descriptive, administrative, file descriptive)
* interactive ingest with decisions
    * file identification choices
    * creating sip (continue, send to backlog, reject transfer)
* every job can be inspected on when started, how long it takes, which file name/uuid, command, output, PRONOM number, error output
* examine content (detect creditcard numbers, etc.)
* send to backlog storage
* backlog tab contains name, transfer uuid, file count, ingest date, you can download or delete the SIP
* appraisal tab (NEW)
    * overview SIP
    * report on objects (types)
    * tag files
    * overview personal identification information, creditcard numbers and such in files
    * previewing files
    * file overview with filters (filetype and such)
    * ArchiveSpace admin/management
    * arranging files in directories
* ingest
    * normalize
        * check for special folders
        * best file type for preservation (make copies for that)
        * ... for access
        * manually
        * create normalization report
        * customize rules for specific types of file in Preservation planning tab
    * choose between AIP storages
* customize default decision inputs
* custom processing configurations

### Exercises
See [the pdf](/Archivematica-exercises.pdf).

### AtoM
* access to memory
* Archivematica was the storage behind AtoM first
* now more separate; AtoM is the user-frontend of the whole system
* multi-lingual support
* multi-repository - many repositories/archives using one single AtoM instance
    * small organisations can use it as well without deploying their own instance
    * Canada - provincial portals
* AtoM-camp in May in Cambridge
* idea for EASY-webui: popups for input fields in UI with explanation, according to standards
