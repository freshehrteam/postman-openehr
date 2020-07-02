title: "Getting ready with Postman" permalink:
PM1-postman-ehrscape-getting-ready.html summary: This section contains
an introduction to the Postman Tool. This tool can be used to run API
calls to send and receive data from the Ehrscape Clinical Data
Repository ---

First you need to install a copy of the API runner application
***Postman*** (Chrome/MacOS/Windows)

[Get Postman Application](http://getpostman.com)

This lets you send and receive data from the Ehrscape API without the
need for a specific programming language.

Postman also allows you to import a preset collection of API calls which
we can use to supply a copy of the Ehrscape API and associated
'environment' file, which contains settings for a specific ehrscape
domain.

# A. Run Postman

Click the 'Run Postman Button' to import the Postman 'openEHR Ehrscape
Clinical Data Repository' API collection and associated ***Operon
Sandpit*** environment settings.

![Run in Postman](https://run.pstmn.io/button.svg)

This will automatically install the Ehrscape Collection and Operon
Sandpit environment files.

# or B. Download Postman files from Git

Click on these links to download the files to your system:

  - [openEHR Ehrscape
    Collection](https://raw.githubusercontent.com/operonsys/postman-ehrscape/master/openEHR%2520Ehrscape%2520Clinical%2520Data%2520Repository.postman_collection.json)

  - [Operon Sandpit
    Environment](https://raw.githubusercontent.com/operonsys/postman-ehrscape/master/oprn_t1_Sandpit.postman_environment.json)

# or C. Download your collection files from email

If you have received an email containing the collection and environment
files to use with Postman. The first step is to download these files
ready to then be imported into Postman.

Find `openEHR Ehrscape Clinical Data Repository.postman_collection` in
your email and download it to a folder of your choice (normally the
Download folder).

Find `<your_environment_name>.postman_environment` in your email and
download it to a folder of your choice (normally the Download folder).
Please note that for demonstration purposes we are using the `C4H Ripple
OSI` environment in this document.

# Import Downloaded files into Postman

If you have downloaded files from Github of from your email, these now
need to be installed in Postman.

Open Postman and select ***Import***

![Import Files into Postman](/images/ImportFilesIntoPostman.jpg)

Locate your two save files and import them. You can either use the
***Choose Files*** option to import one at a time or drag and drop the
files into the window

![Drop Files into Postman](/images/DropFilesInPostman.jpg)

In the top right hand corner, change the environment to your environment
(in the screenshot below that’s the C4H Ripple OSI environment)

![Change environment](/images/SelectEnvironment.jpg)

On the left hand side you can now see the collection files

![Collection](/images/Collection.jpg)
