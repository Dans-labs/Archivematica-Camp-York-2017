Day 3
=====

Deployment practices for development and production
---------------------------------------------------
[deployment documentation](https://www.archivematica.org/en/docs/archivematica-1.6/admin-manual/installation/installation/#installation)

* couple approaches
    * manual using Ubuntu/Centos/Redhat packages
    * using vagrant/ansible
    * puppet, coming in the future (interest from ISH Amsterdam)
* the vagrant installation gives the option to install from a particular branch to check out new features
* support for Digital Ocean droplets
* [archivematica google group](https://groups.google.com/forum/#!forum/archivematica)
* [archivematica-tech google group](https://groups.google.com/forum/#!forum/archivematica-tech)
* Docker support is coming shortly


### Note to future me
if you install Archivematica using vagrant/ansible (`vagrant up`) and then you call `vagrant halt` and restart vagrant using `vagrant up`, you probably get a `502 Bad Gateway` response in the browser. To fix this, login to the VM using `vagrant ssh` and run `am services status`. An example output of that is listed below.

```
vagrant@am-local:~$ am services status
archivematica-storage-service stop/waiting
archivematica-mcp-server start/running, process 5663
archivematica-mcp-client start/running, process 5668
archivematica-dashboard stop/waiting
basic status complete
```

Try to run `am restart-services` and then again `am services status`.

For each of the services that still didn't start, run `sudo start <servicename>`:

```
vagrant@am-local:~$ sudo start archivematica-storage-service
archivematica-storage-service start/running, process 5847
vagrant@am-local:~$ sudo status archivematica-storage-service
archivematica-storage-service start/running, process 5847
vagrant@am-local:~$ sudo start archivematica-dashboard
archivematica-dashboard start/running, process 5879
vagrant@am-local:~$ sudo status archivematica-dashboard
archivematica-dashboard start/running, process 5879
```

Now running `am services status` should show all services running:

```
vagrant@am-local:~$ am services status
archivematica-storage-service start/running, process 5847
archivematica-mcp-server start/running, process 5663
archivematica-mcp-client start/running, process 5668
archivematica-dashboard start/running, process 5879
basic status complete
```

Probably the problem is the version of VirtualBox we currently use (*dependent on EASY deployment???*)


Automation tools
----------------
* simpelest way to automate Archivematica workflow is to answer the questions in the Administration/Processing Configuration tab
* [automation tools Github repo](https://github.com/artefactual/automation-tools) contains the basic instructions and automation tool examples (also notice the branches on this repo)
* configure transfer source locations in storage service
* automated workflows can be triggered differently per transfer source location
* set up email notification when question needs to be answered during a workflow
* @ekoi: [automation for Dataverse](https://github.com/artefactual/automation-tools/tree/dev/dataverse/transfers/examples/pre-transfer)

### Demo
* in storage services registered two transfer source locations, one manual, one auto
* in dashboard both show up in the Transfer/Browse tab
* auto: drop stuff in a folder and have them ingested automatically
* looks all quite similar to our `easy-ingest-flow`


Customizing the FPR
-------------------
* format-version corresponds to a PronomID in archivematica (preservation planning tab)
* file identification microservice
    * FIDO
    * Siegfried
    * file extension Python script
        * script can be editted in the UI to do what you want to do exactly
        * stored with version control
* characterization
    * determining technical metadata from a file
    * characterization rules
* [exercises](exercises/Customizing%20the%20FPR.pdf)


Archivematica roadmap and upcoming developments
-----------------------------------------------
TODO


Project community and governance talk
-------------------------------------
TODO
