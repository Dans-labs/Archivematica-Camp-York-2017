Day 2
=====

Workflow and deployment tours
-----------------------------
Casual chat of how users use Archivematica

### University of Edinburgh
currently:

* test VM
* production VM
* both store AIPs
* users send their data to a shared storage area
* local copy by archivist for pre-ingest procedure (mostly not automated)
* sstc from local copy to production VM for ingest
* stored on tape- and local backup

aspirational:

* user sends (meta)data via browser
* directly into our pre-ingest area
* into production VM with archivematica
* backups (AIPs) offsite
* dspace storage as internal interface (with backup)
* use archivespace as external interface

### University of York
currently:

* everything manual, using checklists

aspirational:

* user deposits data in AtoM
* transfer to archivematica
* appraisal/arrangement
* store in AIP store
* DIP in digital repository (Fedora)
* presented in AtoM

### University of Lancaster
* researchers submits data/metadata
* captured into PURE
* put into archivematica together with metadata (PREMIS); creates preservation and access copies

### University of London
* no archivematica usage yet
* create education package


Metadata deep dive
------------------
(see also https://www.loc.gov/standards/mets/METSOverview.v2.html)

[Slides](slides/Metadata%20deep%20dive.pdf)

PREMIS and METS

* mets file stores metadata
* in an AIP bag it is is the `data/` folder
* PREMIS (preservasion metadata implementation strategies) standard for metadata about objects
* PREMIS events: audit trail
* relations between objects
* METS (Metadata Encoding and Transmission Standard): wrapper for PREMIS
    * METS header
        * info about the METS file (who created it and when, last modified (for versioning))
    * descriptive metadata
        * container for dublincore metadata
        * >1 of these for versioning and such
    * administrative metadata
        * technical metadata container with PREMIS object
        * rights metadata container with PREMIS object
        * provinance (PREMIS events/agents)
            * events linked to agents (institution, logged-in user, digital preservation system)
    * file section
        * everything AIP in detail
        * tells role of particular object (original, license, submissionDocument, preservation, ...)
        * links files to related files using groupIDs
    * structural map
        * layout of the AIP in terms of directories and files/items
* transfer METS file contains data about original transfer (which might end up in multiple SIPs)
* METS makes complex queries over many datasets possible
* Archivematica stores way more in METS than it uses. Just for later usage


Technical architecture overview
-------------------------------

[Slides](slides/Technical%20architecture%20overview.pdf)
[Slides](http://bit.ly/am_arch)

* archivematica accepts files
* flow
    * ingest
    * verify
    * identify
    * chracterize
    * arrange
    * normalise
    * describe
    * package
* uses
    * PREMIS
    * METS
    * Bagit
    * SHA256
    * UUID
* output
    * DIP
    * AIP
* in archivematica using UI or webAPIs
* workflow
    * database
    * dashboard
    * Gearman
    * MCP server
    * MCP client (workers connect to Gearman)
* django
* ElasticSearch index
* FPR server (service for new commands to be running)
* Github:
    * Artefactual
        * Archivematica
        * sample data **<-- idea for EASY!!!**
        * binder (digital repository for museum collections)
        * AtoM
        * storage services
        * METS validator **<-- a variant might be interesting for EASY**
        * <others>
    * Artefactual Labs
        * new/R&D things
        * acceptance tests (selenium tests with Gherkin files)
        * ansible-role repos
        * rpm package scripts
        * METS reader/writer **<-- analogous to our plans for DDM/EMD?**
* https://wiki.archivematica.org/Micro-services
* microservices contain jobs
    * jobs are python scripts
    * microservices link jobs together
    * everything stored into database
    * it's not 'microservices' as we understand them!


Storage service management
--------------------------

* storage service separated from Archivematica
* pipeline
    * archivematica installation
    * multiple pipelines are possible in the storage system
    * credentials need to be exchanged
* spaces
    * arbitrary way to describe a storage system
    * might be a filesystem
    * can also be something like Dataverse, Fedora, etc.
* locations
    * a portion of the space where to store the stuff
* packages
    * an AIP, DIP or transfer


Validation micro-service developments
-------------------------------------

[Slides](slides/Validation%20micro-service%20developments.pdf)
[MediaConch](https://mediaarea.net/MediaConch/)
[MediaConchOnline checker](https://mediaarea.net/MediaConchOnline/checker)

* MediaConch used for validating video files.
* making sure the files are valid
* mkv file is a container format with multiple video, audio, text streams
* enforce technical details of the video
* conform to your own policy
* this will probably be in Archivematica 1.7
* plans to do similar things with PDF
