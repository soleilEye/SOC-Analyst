Cyber Threat Intelligence is typically a managerial mystery to handle, with organisations battling with how to input, digest, analyse and present threat data in a way that will make sense. There are numerous platforms that have been developed to tackle the juggernaut that is Threat Intelligence. (Существует множество платформ, которые были разработаны для борьбы с такой безжалостной силой, как Threat Intelligence.)

## OpenCTI
[OpenCTI](https://github.com/OpenCTI-Platform) is another open-sourced platform designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs.

<p align="center">
  <img src="https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/OpenCTI/Images/logoOpenCTI.png">
</p>

### Objective
Developed by the collaboration of the [French National cybersecurity agency (ANSSI)](https://www.ssi.gouv.fr/), the platform's main objective is to create a comprehensive(всесторонний) tool that allows users to capitalise on technical and non-technical information while developing relationships between each piece of information and its primary source. The platform can use the [MITRE ATT&CK framework](https://attack.mitre.org/) to structure the data. Additionally, it can be integrated with other threat intel tools such as MISP and TheHive.

<p align="center">
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/OpenCTI/Images/DashboardOpenCTI.png>
</p>

### OpenCTI Data Model
OpenCTI uses a variety of knowledge schemas in structuring data, the main one being the Structured Threat Information Expression (STIX2) standards. STIX is a serialised and standardised language format used in threat intelligence exchange. It allows for the data to be implemented as entities and relationships, effectively tracing the origin of the provided information.

This data model is supported by how the platform's architecture has been laid out. The image below gives an architectural structure for your know-how.

<p align="center">
  <img src=https://github.com/AM1RKA/SOC-Analyst/blob/main/Cyber%20Threat%20Intellegence/OpenCTI/Images/OpenCTIModel.png>
</p>

The highlight services include:

* **GraphQL API**: The API connects clients to the database and the messaging system.
* **Write workers**: Python processes utilised to write queries asynchronously from the RabbitMQ messaging system.
* **Connectors**: Another set of python processes used to ingest, enrich or export data on the platform. These connectors provide the application with a robust network of integrated systems and frameworks to create threat intelligence relations and allow users to improve their defence tactics.
According to OpenCTI, connectors fall under the following classes:

| Class	 | Description | Examples |
|:-------------:|:------------:|:------------:| 
| External Input Connector | Ingests information from external sources | CVE, MISP, TheHive, MITRE |
| Stream Connector | Consumes platform data stream | History, Tanium |
Internal Enrichment Connector (Внутренний соединитель обогащения) |	Takes in new OpenCTI entities from user requests |	Observables enrichment |
Internal Import File Connector |	Extracts information from uploaded reports |	PDFs, STIX2 Import |
Internal Export File Connector |	Exports information from OpenCTI into different file formats |	CSV, STIX2 export, PDF |

Refer to the [connectors](https://github.com/OpenCTI-Platform/connectors) and data model documentation for more details on configuring connectors and the data schema.
