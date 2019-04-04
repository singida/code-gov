# Infrastructure (Work in Progress)

This file describes the infrastructure, server space, and memory required to run Code.gov.  It breaks down the server requirements by different front-end and back-end processes.

# front-end
The front-end of Code.gov is currently a static site that can be found at code-gov-web.

# back-end
The back-end consists of the following different parts:

1. Harvester
1. API
1. Elastic Search

All of these applications/services can be deployed on independent servers/containers and/or a single server.  The following diagram illustrates the current implementation of these applications.

![Architecture Diagram](images/back_end_architecture.png)

## Harvester
The Harvester application uses a meta-data json file to locate various agency code.json files.  The code.json file contains a list of various projects and their related details.  For each agency, the Harvester reads the code.json file for content, validates the format, ranks the project based on pre-defined criteria and refreshes multiple Elastic Search indices.

The meta-data file (json) and agency code.json files can be located anywhere on the file system or internet accessible URL.  The location of the meta-data file can be configured as a part of the Harvester configuration.

The location of the Elastic Search server/service is also configurable as a part of the Harvester configuration.

## API
The API application uses the data stored in the Elastic Search indices and presents them as appropriate API endpoints.  These API endpoints can be used by a front-end and/or mobile application to further render that particular application

The location of the Elastic Search server/service is configurable as a part of the API configuration.


## Elastic Search
The Elastic Search engine is the de facto storage used by both the Harvester and API applications.  The Harvester application creates/updates various indices and the API application reads these indices to deliver data for its various endpoints.
