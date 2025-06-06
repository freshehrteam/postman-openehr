title: "Overview of openEHR and Ehrscape" permalink:
ES0-overview-openehr-ehrscape.html summary: This section provides an
overview of the basic concepts of openEHR and introduces the Operon
Ehrscape service ---

# Introduction

openEHR is a open specification for the information model of an
electronic health record, published and maintained by the [openEHR
Foundation](http://openehr.org).

The full openEHR specification is complex and beyond the scope of this
simple overview. In summary, an application developer interacts with an
an openEHR system and a standardised information model via a simple set
of ‘service’ APIs.

openEHR does not itself create and publish EHR solutions or
applications, rather it provides a specification for a key part of the
technology stack on which other developers base their systems. The value
of this approach is in reducing the effort to meet the needs of
continually changing clinical requirements while increasing the
likelihood of interoperability.

The information model and querying/persistence are defined separately
via the use of shareable (normally open-sourced) archetypes and
templates, There is no direct interaction with the persistence layer,
instead all of the interactions with an openEHR system, including
querying happens via the information model. In essence this is not
dissimilar to the kind of abstraction provided by Django or Ruby Active
Objects, but is designed to work with the health domain, is much more
extensible, and is designed to work in a completely language and
technology-neutral manner.

openEHR systems can be built on any programming language, OS platform
and with any persistence solution - examples of SQL Server, Oracle,
PostgreSQL, mongoDB and MumpsDB solutions exist. It is the
responsibility of the back-end developer to map their chosen persistence
solution to the openEHR information model and querying system.

Ehrscape is an API wrapper for an implementation of the
[openEHR](openehr.org) specification.

The overall structure of an openEHR clinical system is …

    Physical CDR
     Virtual CDR (Ehrscape Domain)
      EHR
       (FOLDER)
        COMPOSITION
         (SECTION)
          ENTRY
           (CLUSTER)
            ELEMENT
             name
              value

## CDR - Care Data Repository

All of the records within a single namespaced patient data repository.
In the Ehrscape environment, a single physical repository is represented
as a number of independent virtual ‘domains’ each of which can be
regarded as a separate CDR.

## EHR - Electronic Health Record

The top-level container of all clinical records for a single patient.

## FOLDER (optional)

A high-level grouping of Compositions. Not implemented in Ehrscape, and
not in common use generally

## COMPOSITION

A document-level container for all clinical records. This equates to an
Encounter, a Lab Report, a Discharge summary, a set of Nursing
Observations. All openEHR data is stored within the context of a
composition and always includes clinical/medico-legal context such as
patient, clinical author details, encounter times etc.

The Composition is the container for structured/ coded data with
granular clinical statements such as procedure, blood pressure, allergy
expressed as an ENTRY, within which the leaf data is contained in
ELEMENTS e.g Systolic, Diastolic, Cuff size.

Compositions are versioned and fully-audit trailed, so that previous
versions can always be retrieved.

Two forms of persistence/versioning strategy can be employed

1.  **‘Event document’ strategy**
    
    Most compositions will be saved as ‘events’. Each instance of the
    event creates an entirely new composition with a new unique
    identifier. This equates to a POST in Restful terms. Examples would
    be a GP encounter, Nursing observation or Discharge report. Updated
    versions of these kinds of documents would only be created if an
    error or inaccuracy needed to be corrected.

2.  **‘Curated document’ strategy**
    
    A less common, but important versioning strategy involves ‘curated
    documents’ where it is important to hold a single instance of a
    named document, but which requires to be continually updated as a
    ‘source-of-truth’. Examples might be a Problem summary, a list of
    known allergies, or an End-of-Life Care Plan. The common factor with
    these type of documents is that there should only ever be a single
    instance which reflects the current known facts or understanding. Of
    course previous versions must remain accessible for medico-legal
    purposes.

### Versioning

openEHR systems handle versioning automatically. Any time a new version
of an existing document is committed to the system, its unique
compositionId identifier ‘version suffix’ is updated e.g

    798e27b1-f2e8-48c3-8ced-42d4d27d1db3::c4h.hopd.com::1

→

    798e27b1-f2e8-48c3-8ced-42d4d27d1db3::c4h.hopd.com::2

In normal operation only the most recent version of the composition is
returned by querying or composition retrieval.

## SECTION (optional)

Sections are optional structures which are used to break up complex
openEHR Compositions, grouping the Entries into high-level headings e.g.
in a Transfer of Care document, Sections might be represented as
Allergies, Problems, Procedures, Lab tests etc. Sections are convenient
for human consumption and navigation but should not be used to infer
meaning.

## ENTRY

In openEHR, all of key clinical content is carried within one of the 5
ENTRY sub-classes:

  - OBSERVATION

  - EVALUATION

  - INSTRUCTION

  - ACTION

  - ADMIN\_ENTRY

The ENTRY is the container for structured/ coded data via granular
`clinical statements` such as Procedure, Blood pressure, Allergy within
which the leaf data is contained in ELEMENTS e.g Systolic, Diastolic,
Cuff size.

## CLUSTER (optional)

A Cluster is a branch-like sub-structure of an ENTRY which allow
ELEMENTS to be conveniently grouped and possibly repeated e.g in a Lab
Test archetype, data related to a single lab analysis result is grouped
within a Cluster to allow the whole pattern to be repeated

  - Lab Test

  - Lab Result (Cluster)

  - Result

  - Comment

  - Datetime reported

  - Status

In the construct above the cluster allows multiple Lab results to be
captured within a single Lab Test.

## ELEMENT

An Element is the leaf-node construct which is basically a name/value
pair with a defined datatype. The nature of the datatype determines the
exact structure of the Element.

# Operon Ehrscape domains and EhrExplorer

The [Operon Ehrscape](https://test.operon.systems) openEHR service
provided by [Marand](http:/marand.si) is configured to allow app
developers to setup and work their own individual `domain`, populated
with its own dummy patient data and openEHR content models and allows
both read and write access to the data and for the upload of new openEHR
content models.

Each Ehrscape domain has its own login and password and in the near
future may also be accessed via an Ouath2 session from trusted provider.

There are 2 methods of accessing the ehrscape API

1.  Set up a sessionID variable via the GET /session call. This returns
    a token that can be supplied in the headers of any subsequent API
    calls. This is the preferred option since it avoids having to log in
    to Ehrscape for every separate API call.

2.  Create a Basic Authentication string and pass this to each API call.
    This is simpler to work with, particularly where it is not easy to
    maintain a session variable e.g. in an API testing tool like Postman
    but incurs an overhead of having to resolve the username and
    password for each call.

## Requesting an Ehrscape domain

You can request an Ehrscape Domain via the Operon website. You will need
to be a registered Operon user and access to your Ehrscape domain will
require your Operon login and password. You will also need to provide a
simple, unique `domain name` such as `freshehr` or `cerner`. This will
be used to create a unique internal server name such as
`ehrscape.operon.ehrscape` used internally by Ehrscape.

An example of an ehrscape Domain that is being used for C4H Training
might be

    login: operon_training
    password: 223ergt$
    domain_name: ehrscape.c4h.training

### baseURL

The baseURL for all Operon Ehrscape API calls is
<https://test.operon.systems/rest/v1>.

## Domain provisioning

When your domain is setup you will be provided with the following

1.  Access to a personal domain on Operon Ehrscape with login, password
    and domain name.

2.  Access to the Ehrscape EhrExplorer tool.

3.  Acess to the Ehrscape ApiExlorer tool.

4.  The domain will be populated with
    
      - Several dummy patents
    
      - openEHR content models and dummy data for
    
      - Nursing Vital signs encounter.

## EhrExplorer

![EHR Explorer](/images/ehr_explorer.png)

The Marand EhrExplorer tool can be used to create openEHR queries and to
visualise the openEHR content models being used by your domain

1.  Browse to [EHRExplorer](https://test.operon.systems/explorer/)

2.  Enter the name and password for your C4H Ehrscape domain as above

3.  Leave the domain field as `ehrscape`

In the navigation bar on the left you can double-click on the `Vital
signs encounter` template, which will open the template in the
bottom-right panel. Right-click on nodes for further details of the
constraints applied.

e.g. If you navigate to **'$$$'** and right-click you can examine the
internal *'atcode'* constraints allowed for this element.

## Ehrscape API browser

1.  Browse to [EHRScape API
    Explorer](https://test.operon.systems/api-explorer.html)

2.  Press the ![Tool button](/images/tool_button.png) tool setting
    button and set userName to `c4h_train` and password to `c4h_train99`

3.  Any test calls in the API browser will now work against the Operon
    Training domain.

## Using Postman to test API calls

The [Postman add-on](http://getpostman.com) is vey useful for testing
API calls outside of an application context. [Postman collection and
environment files](/technical/postman) are available for the C4H. The
collection file contains all of the relevant Ehrscape API calls and a
Postman Environment file matching your domain details will be created
and which you may import.
