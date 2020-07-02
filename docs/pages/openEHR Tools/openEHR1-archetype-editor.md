title: "Archetype Editor" permalink: openEHR1-archetype-editor.html
summary: This section provides instructions on how to install and
configure the Archetype Editor tool and download the archetypes from the
international CKM repository ---

# Install Archetype Editor

The Archetype Editor is the tool we use to create and adapt archetypes.

![Archetype Editor](/images/ae_screen.png)

Download the [latest
version](http://www.openehr.org/download_files/archetype_editor/archetype_editor_2.8.972.1-windows_32bit.exe)
of Archetype Editor.

This installs the openEHR Archetype Editor (ArchetypeEditor.exe) in the
folder …

  - Windows-32  
    C:\\Program Files\\openEHR\\Archetype Editor

  - Windows-64  
    C:\\Program Files(x86)\\openEHR\\Archetype Editor

and should set up links on your Desktop or Start Menu etc.

Further details are available at the [openEHR Archetype Editor Download
page](http://www.openehr.org/downloads/archetypeeditor/home).

# Setup Archetype Editor

1.  Run the Archetype Editor from the Desktop or Start Menu.

2.  At the initial screen, open any existing archetype on your system
    e.g. one of the CKM archetypes previously downloaded
    
        ..\Documents\openehr_training\remote\ckm\archetypes\cluster\OPENEHR-EHR-CLUSTER.device.v1.adl
    
    Or one of the sample archetypes provided at
    
        ..\Users\Public\Documents\My Clinical Models\Sample Set\Archetypes

## Set the default Archetype Editor paths

![Archetype Editor setup](/images/ae_tool_setup.png)

Go to ***Tools→Options→File Locations*** and set both

  - ***Archetype Repository path***

and

  - ***Archetype XML Repository path***

to

    ..\Documents\openehr_training

## Setup User Defaults

![User Setup](/images/ae_user_setup2.png)

Go to ***Tools→Options→User Defaults*** and enter your details.

|              |                                   |
| ------------ | --------------------------------- |
| Name         | Ian McNicoll                      |
| Email        | <ian@freshehr.com>                |
| Organisation | freshEHR Clinical Informatics, UK |

e.g.

# Download Archetypes

The openEHR Foundation Clinical Knowledge Manager (CKM) is a web-based
tool that stores openEHR clinical models that are developed
collaboratively by the openEHR community and made freely available for
others to use and copy.

![CKM Bulk Export](/images/ckm_export.png)

Go to [openEHR Foundation CKM](http://openehr.org/ckm) then from the top
menu select ***Archetypes→Bulk Export***.

This will create a zip file with the latest versions of openEHR
Foundation CKM archetypes.

Download this zip file and unzip it into the remote/ckm folder you
created earlier e.g.
***..\\Documents\\openehr\_training\\models\\remote\\ckm\\archetypes***
making sure you preserve the folders.

You should now have something like

    openehr_training
     local
        archetypes
        templates
     remote
        ckm
         archetypes
          cluster
            composition
            demographic
            entry
            section
            readme.txt

Depending on how your zip program works you may need to move the
unzipped folders around to match this pattern.

## CKM ‘GitHub mirror’

Git is a common software version control tool. The CKM archetypes and
templates are ‘mirrored’ out to a Git repository hosted at the [openEHR
Github](https://github.com/openEHR/CKM-mirror).

![GitHub](/images/Octocat.png)

If you are familiar with using Git, you can clone the repository as `git
clone https://github.com/openEHR/CKM-mirror.git`.
