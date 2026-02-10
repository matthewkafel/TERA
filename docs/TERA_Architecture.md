# TERA Memo Architecture Documentation

> **Automatically extracted from PDF for GitHub Copilot ingestion**  
> **Source**: TERA Memo Architecture PDF  
> **Total Pages**: 17  
> **Extraction Date**: 2026-02-10

## Document Metadata

- **Status**: Final - updated for 8/18/25 submission
- **Review Date**: 4/4/25
- **BIP Tenant Boundary**: Compensation and Pension UI
- **System Acronym**: CPUI
- **VASI ID**: 3028
- **Deployment Date**: 26 January 2025

---

## Table of Contents

- [Page 1: TERA Memo Architecture](#page-1)
- [Page 2](#page-2)
- [Page 3: Use Cases](#page-3)
- [Page 4](#page-4)
- [Page 5](#page-5)
- [Page 6](#page-6)
- [Page 7](#page-7)
- [Page 8](#page-8)
- [Page 9](#page-9)
- [Page 10](#page-10)
- [Page 11](#page-11)
- [Page 12: Conceptual Data Viewpoint Model (DIV-1)](#page-12)
- [Page 13: Physical Data Viewpoint Model (DIV-3)](#page-13)
- [Page 14](#page-14)
- [Page 15](#page-15)
- [Page 16](#page-16)
- [Page 17](#page-17)

---

<a name="page-1"></a>

## Page 1: TERA Memo Architecture

TERA Memo Architecture
Documentation
Status
Final - updated for 8/18/25 submission
Review Date
4/4/25
BIP Tenant
Boundary
Compensation and Pension UI
BIP Tenant
Component
tera
System
Acronym
CPUI
VASI ID and Link
3028
BIP Tenant App
(s)
bip-
-tera-memo-ui
cpui
GitHub Link(s)
https://github.com/department-of-veterans-affairs/bip-tera-memo-automation
https://github.com/department-of-veterans-affairs/bip-cpui-tera-memo-ui
BIH Link(s)
Compensation and Pension UI
MSR Links(s)
2429
Solution and
support Links
Solutioning: TERA Memo Solution Document
Sponsoring
organization
VACO
Number of users
Approx. 30k potential unique users; Through-put of total users on any given day approximately 5k.
Estimated
Monthly Cost
Estimated monthly costs:
AWS SageMaker: ~$7,000
 TBD
CPUI Namespace:
Privacy
PII: Veterans name and file number; non-veterans are not applicable to TERA Memo
PHI: Medical data from documents in eFolder is reviewed but the data itself is not stored, only references to documents. PHI may
be stored based on the final text submissions made by the user.
Will need 508
Compliance
Yes
Deployment date
26 January 2025
eMASS ID
(System Name)
2049 (BIP Compensation and Pension User Interface)
Introduction
The TERA Memorandum form enables the Department of Veteran Affairs to expedite TERA Memorandum processing, incurring significant time savings for
Veteran Service Representatives (VSR) reviewing as well as the Veteran claims processing. Additionally, TERA Memorandum Automation serves to
solution and implement technology focused on Artificial Intelligence initiatives to provide the Department of Veteran Affairs with software that can offer
problem-solving and decision recommendation capabilities in support of streamlining and standardizing the TERA Memorandum claim reviewal process.
Key Definitions
Toxic Exposure Risk Activity
TERA:


---

<a name="page-2"></a>

## Page 2

VSR: Veteran Service Representative who supports claim processing of TERA Memorandums
AWS SageMaker: Allows for building and deploying models
Artificial Intelligence (AI) systems are defined as: "Any artificial system that performs tasks under varying and unpredictable circumstances

without significant human oversight, or that can learn from experience and improve performance when exposed to data sets." AI Systems
Generally function by generating predictions, classifications or recommendations, or generating new content from inputs provided by the user or
underlying applications (VA AI Inventory).
Optical Character Recognition (OCR): technology that converts scanned documents and images into machine-readable text. VBMS
SmartSearch solution provides this capability.
Key Capabilities
Enhance efficiency of completing TERA Memorandum forms with available data from a Veteran's Claim Evidence.
Provide pathway for future AI use cases on BIP Platform.
Intended Value
The TERA Memorandum Automation functionality intends to deliver the value of enhanced efficiency to VSRs processing TERA Memorandum
forms with the potential to 675,000 annual labor hours for users to spend on higher value activities that require their expert judgement.
Key Features
The below key features collectively support the MVP Scope delivery of TERA Automation ART as outlined in
 .
 -


BPT-4018
Capability to Automatically Populate TERA Memo Questions Using Claims Evidence Data
DONE
Modernized TERA Memorandum form User Interface with 508 Compliance
Auto-Population button at the top of the TERA Memorandum UI to auto-populate certain questions within the form using evidence stored in the
Veteran's Claim Evidence
Add links to specific locations within Claim Evidence documents for manual review for each auto-populated answer
Add confidence score for each auto-populated answer
Gathering of metrics for submitted TERA Memorandum answer selections
Monitoring Dashboard for tracking performance
Feature flag functionality to enable/disable: Legacy & Modernized forms, Auto-Population Button, & Metrics gathering
AI Inventory Alignment
TERA Memorandum automation aligns to the VA AI Inventory use case of Human-Like Capabilities and is Rights Impacting. The TERA Memorandum
Automation VA AI Inventory use case was submitted in August 2024.
Human-Like Capabilities: Developed in software, hardware or other context to solve tasks requiring
human-like perception, cognition.
Rights Impacting: AI Systems whose outputs form the basis for decisions or actions that have
legally significant effects on an individual's or entity's civil rights,
liberties, privacy, or access to essential opportunities.
Use Case View
As a Veteran Service Representative (VSR), I need to process Veteran claims for Toxic Exposure Risk Activity (TERA) so that I can identify if a Veteran
meets the criteria for TERA related activities.
Capability Viewpoint Vision (CV-1) (VASI Description)
TERA Memorandum Automation (TERA Automation) resides on Benefits Integrated Platform as a Service (BIP- #2295) and is under the Compensation
TERA Memo UI enables VSR to leverage Artificial Intelligence in completing initial TERA Memo processing. VSRs

 (CPUI-3028) Product.
and Pension UI
will be able to initiate auto-population of evidence gathered that is relevant to TERA Memo intake. Given a confidence score as well as links to specific
locations within document evidence for manual review, VSRs can efficiently assess and certify the validity of evidence gathered.
Capability Viewpoint Taxonomy (CV-2)


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Capability Viewpoint Taxonomy (CV-2): Hierarchical tree showing TERA Memo capabilities including auto-population, AI integration, and BIP platform services

![Capability Viewpoint Taxonomy (CV-2): Hierarchical tree showing TERA Memo capabilities including auto-population, AI integration, and BIP platform services](docs/images/page_2_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-3"></a>

## Page 3: Use Cases

Use Cases
The below diagram outlines the expected behavior of the Veteran Service Representative (VSR) while within VBMS completing a TERA Memorandum
form.
User Interface Functionality
The TERA Memorandum Form was modernized to follow updated VBMS standards for user interface and experience in line with 508 compliance
standards. Design updates include:
Modernized User Interface Design
Veteran Information pre-populated
Addition of auto-population user interface components including:
Auto-Population button
Auto-Population information modal on buttons election
Checkbox of manual review of auto-populated recommendations
Policy change updates to TERA Memorandum for questions and answers.
Access to the TERA Memorandum Form is controlled through VBMS Document Policy on the Veteran Profile that will show the TERA Memo as a
drop-down action when the end user has the ability to Upload a document.
Auto-Population Functionality
TERA Automation utilizes algorithms to provide recommended decisions to support completing the TERA Memorandum form.


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: VSR Workflow Diagram: Complete user journey showing 14 steps from opening VBMS to submitting TERA Memo, including auto-populate decision point, evidence review, and validation

![VSR Workflow Diagram: Complete user journey showing 14 steps from opening VBMS to submitting TERA Memo, including auto-populate decision point, evidence review, and validation](docs/images/page_3_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


**Diagram 2**:


**Diagram Description**: User Interface Components: Wireframe showing form layout with auto-populate button, confidence score badges, evidence links, and manual review certification checkbox

![User Interface Components: Wireframe showing form layout with auto-populate button, confidence score badges, evidence links, and manual review certification checkbox](docs/images/page_3_diagram_2.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-4"></a>

## Page 4

a.
b.
c.
Input: Data & eligibility sources
Data extracted from Veteran's Claim Evidence documents via C&P Smart Search Optical Character Recognition (OCR) scans
Data extracted from Veteran's ILER IES record
PACT Act Standard Operation Procedures
VA Guidance from the M21-1 Adjudication Procedures Manual
Model:
Algorithms that analyze and interpret the input data, leveraging AWS SageMaker via the ML-MATS Platform, applying the eligibility
requirements and guidelines from the PACT Act SOP and M21-1 to the Veteran's Claim Evidence
Output: Evidence in support of "Yes" answer to Questions 1, 3, 4 and/or 6:
Determination of "Yes" selection on form
Open-Text field response with supporting details
Linked to
 identified document(s) and Confidence Score for manual review
specific locations within document evidence
Model Processing
Daily Batch Process
As part of this daily batch process, documents added to the evidence folder are converted from Image or PDF to text files. These text
files are then added to the OpenSearch database and indexed.
The final step in this daily process is to run the TERA Model, which queries evidence in the OpenSearch Database and then writes the
answers to the TERA Memo data table.
This data table can then be queried by the TERA Memo UI to support auto-population.
Main Actors
The following table describes the actors listed in the diagram as a user in the scope of the TERA Memorandum Automation architecture.
Name
Description
VSR
The individual tasked with VBMS claim processing including the TERA Memorandum form.
Systems Details
The following table describes the system details for TERA Memorandum Automation.
System
Description
VBMS CPUI
Contains the React / Micro Front End TERA Memo UI
Claim Evidence (Claim Evidence API)
Source of TERA evidence including a SmartSearch endpoint that houses OCR results from eFolder documents
VBMS Core DB
Repository of Veteran data. Leveraged during the auto-population process
ML-MATS Platform (AWS
SageMaker)
Houses AI models used to automate evidence gathering and uses CICD pipelines to deploy to upper
environments
Main User Functions
VSR will be able to use the auto populate feature to automate evidence gathering in support of TERA Memo completion.
Actor
Description
Usage


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: AI Model Pipeline: Three-stage process showing Input (claim evidence, ILER, PACT Act SOP), Model (AWS SageMaker processing with NLP), and Output (recommendations with confidence scores and evidence links)

![AI Model Pipeline: Three-stage process showing Input (claim evidence, ILER, PACT Act SOP), Model (AWS SageMaker processing with NLP), and Output (recommendations with confidence scores and evidence links)](docs/images/page_4_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-5"></a>

## Page 5

VSR
The VSR is tasked with
completing the TERA
Memorandum form questions
in VBMS.
After selecting the auto-population button, the VSR will manually review the recommended answers and
linked evidence documents retrieved from artificial intelligence (AI) models along with confidence score of
results and update the answers as needed before previewing and submitting the form.
TERA
Memorandum
Questions
Details
Question 1
Question 1 text:
"Does the Veteran qualify for a presumption of exposure(s) for one or more of the following hazards during military service? (If Yes,
provide details below.)"
 User Response Options:
 - "Yes, the Veteran was exposed to the following"
 - "No, the Veteran was not exposed to the following"
 If "Yes" is selected:
 The user must indicate at least one of the following hazards, presented with checkboxes (multiple selections are allowed):
 - Herbicide Agent - 2,3,7,8 - Tetrachlorodibenzodioxin (TCDD)
 - Radiation – Ionizing
 - Mustard Gas - Nitrogen, Sulfur Mustard, or Lewisite
 - Camp Lejeune Water Contamination - Perchloroethylene (PCE), trichloroethylene (TCE), vinyl chloride, benzene
Under question 1 checkboxes, the user has the ability to enter a free text response, the following prompt is provided: “Evidence of
exposure (include the subject and date of receipt of the cited documents):”
Question 2
Question 2A text:
“Is there an Individual Longitudinal Exposure Record (ILER) entry for the Veteran? (If
ensure documentation is uploaded in
 No,
VBMS. If
, answer 2B and ensure that the ILER (Individual Exposure Summary (IES)) Report is uploaded into VBMS.
Nam
 Yes
 Note:
e only, contractor, and civilian entries are not TERAs; select
in these circumstances.)"
 No
Question 2A user response options:
- "Yes"
- "No"
Question 2B text:
“Is there an ILER entry for an activity carried out by the Veteran while on active duty involving toxic exposure to occupational or
environmental hazards? (If Yes, answer 2C as well. If No, select the type(s) of ILER entry(ies) of record that were determined to not
involve toxic exposure during active duty, and provide justification for this determination in the free text box below. See “TERA
Exception Job Aid” for more information on the circumstance-based exceptions.)”
Question 2B user response options:
- "Yes"
- "No, the ILER entry(ies) do not involve toxic exposure (select all that apply)"
Under the “No, the ILER entry(ies) do not involve toxic exposure (select all that apply)” response, there are two checkboxes:
- “Do/does not corroborate toxic exposure to occupational or environmental hazards”
- “Consist(s) of self-reported information that cannot be substantiated”
Under question 2B checkboxes, the user has the ability to enter a free text response, the following prompt is provided: “Explanation
of determination:”
Question 2C text:
“Is there any evidence of exposure over permissible limits or of concern (identified in red text) in the ILER report? (If Yes, ensure
that pertinent evidence is bookmarked or annotated in VBMS. For more information, see Exposure Levels that Exceeded
Permissible Levels in “ILER Guidance.”)”
“TERA Exception Job Aid” in the final sentence of the question contains a link to - TERA Exception Job Aid.pdf
Question 2C user response options:
- "Yes"
- "No"


---

<a name="page-6"></a>

## Page 6

Question 3
Question 3A text:
“Does the Veteran's VBMS eFolder contain the Persian Gulf War Service - Sec. 1117 flash and/or 1117 memo? (If No, answer 3B
as well.)”
Question 3A user response options:
- "Yes"
- "No"
Question 3B text:
"Is there evidence of record verifying that the Veteran served in a 38 C.F.R. § 3.317(e)(2) and/or Sec. 1117 location? (If Yes,
provide details below.)"
 Question 3B user response options:
 - "Yes"
 - "No"
Under question 3B, the user has the ability to enter a free text response, the following prompt is provided: “Evidence of service in a
38 C.F.R. § 3.317(e)(2) and/or Sec. 1117 location (include the subject and date of receipt of the cited documents):”
Question 4
Question 4A text:
“Does the Veteran’s VBMS eFolder contain the
flash and/or 1119 memo?  (If
,
 Toxic Exposure – Sec. 1119 Covered Veteran
 No
answer 4B. If
, answer 4C as well.)”
 Yes
 Question 4A user response options:
 - "Yes"
 - "No"
 Question 4B text:
“Is there evidence of record verifying that the Veteran served in a 38 C.F.R. § 3.320 and/or Sec. 1119 location? (If
, answer 4C
 Yes
and provide details below.)”
Question 4B user response options:
 - "Yes"
 - "No"
Question 4C text:
“Does the Veteran’s VBMS eFolder contain the
flash? (If
, answer 4D.)"
 Toxic Exposure-Uzbekistan Deployed Veteran
 No
Question 4C user response options:
 - "Yes"
 - "No"
Question 4D text:
“Is there evidence of service at Karshi-Khanabad (K2)? (If
, provide details below.)”
 Yes
Question 4D user response options:
 - "Yes"
 - "No"
Under question 4D, the user has the ability to enter a free text response, the following prompt is provided: “Evidence of service in a
38 C.F.R. § 3.320 and/or Sec. 1119 location or K2 (include the subject and date of receipt of the cited documents):”
Question 5
Question 5A text:
"Is there evidence of other deployment related exposure in the eFolder (not already depicted in the questions above) which is
consistent with the circumstances of the Veteran’s service? (If Yes, provide details below and answer 5B as well.)”
 Question 5A user response options:
 - "Yes"
 - "No"
Under question 5A, the user has the ability to enter a free text response, the following prompt is provided: “Evidence and details
about deployment related exposure (include the subject and date of receipt of the cited documents):”
 Question 5B text:
 “Where in the eFolder does the deployment information exist (e.g., VIS, military personnel records, DD214, service treatment
records, post-deployment health assessments, PIES responses, etc.)? (Ensure that the pertinent evidence is bookmarked or
annotated in VBMS.)”
Under question 5B, the user has the ability to enter a free text response.


---

<a name="page-7"></a>

## Page 7

Question 6
Question 6 text:
“Is there evidence of non-deployment related exposure in the eFolder which is consistent with the circumstances of the Veteran’s
service? (If Yes, provide details below.)”
Question 6 user response options:
 - "Yes"
 - "No"
Under question 6, the user has the ability to enter a free text response, the following prompt is provided: “Evidence and details
about non-deployment related exposure (must include a description of the specific toxic exposure(s) being conceded, to include any
relevant location, dates, and length of each exposure, etc., and the subject and date of receipt of the cited documents):”
Conclusion
Conclusion part 1 text:
“Did the Veteran participate in a TERA during active military service? (If Yes was answered to any of the above questions, then
"Yes, the Veteran participated in a TERA" should be selected, and Part 2 should be answered as well.)"
Conclusion part 1 user response options:
- "Yes, the Veteran participated in TERA"
- "No, the Veteran did not participate in a TERA"
Conclusion part 2 text:
“Is the TERA participation of record sufficient to trigger an examination/opinion under 38 U.S.C. § 1168(a)? (Important: If 2A is the
only question on the TERA memorandum with a Yes response, then an examination and opinion under 38 U.S.C. § 1168(a) is/are
not warranted and the No answer option should be selected below.)”
Conclusion part 2 user response options:
- "Yes"
- "No, the only participation in a TERA that is established is based on an entry in an exposure tracking record system, such as ILER,
that is deemed an exception under 38 U.S.C. § 1168(b)."
- "No, the Veteran served in a location where exposure to herbicides is conceded. However, herbicide exposure is the only TERA
and the condition has been determined by the Secretary to have no positive association with herbicide exposure."
Under conclusion part 2, the user has the ability to enter a free text response, the following prompt is provided: “Identify the
contention(s) in the text box below:”
Primary Systems High Level Operational Viewpoint (OV-1)
The OV-1 is a high-level graphical/textual description of the operational concept (what happens, who does what, in what order, to accomplish what goal).
The purpose of OV-1 is to provide a quick, high-level description of what the architecture is supposed to do, and how it is supposed to do it (players
/operations involved).
The primary components of the TERA Memo architecture a React Front End, API, and AI components.
VBMS Resource Locations
White Rectangle - TERA application resource to resource being documented
Gray Rectangle -  Existing application resource to resource being documented
The table below describes the lines and arrows in the diagram above:
System A and
VASI ID
System B and

VASI ID
Interaction Description
AWS SageMaker
OpenSearch
Endpoint
Enables the ability to run the TERA model against OpenSearch Veteran Dataset and store in VBMS
Core Database


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: High-Level Operational View (OV-1): System context diagram with TERA components (white boxes) including UI and API, integrated with existing VBMS components (gray boxes) like Claims Evidence API, DocGen, and AWS SageMaker

![High-Level Operational View (OV-1): System context diagram with TERA components (white boxes) including UI and API, integrated with existing VBMS components (gray boxes) like Claims Evidence API, DocGen, and AWS SageMaker](docs/images/page_7_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-8"></a>

## Page 8

Claims Evidence API
VBMS Core
Database
Pulls relevant data on Veteran from VBMS Core Database to support in population TERA Memo UI
Claims Evidence API
TERA Memo UI
Auto-population populates TERA Memo with relevant recommendation for Veteran
ILER API
TERA Memo UI
Retrieves Veteran ILER document used to provide data for auto-population
TERA Memo UI
CE API / CE UI
Ability for user to click evidence link for auto-populated recommendation to manually review specific
locations in document
TERA Memo UI
DocGen GenStore
API
Upload of completed TERA Memorandum Document to Claim Evidence
VBMS
TERA Memo UI
Initiate auto population
Review Recommendation
Validate answers
Operational Resource Flow (OV-2)
The OV-2 is a behavioral diagram that describes the Resource Flows exchanged between "Operational Performers." In other words, it shows the
collaboration of main systems on the key data elements (e.g., system A sends a package while system B receives the package).
Logical View
Implementation of the modernized TERA Memo in VBMS involves three core concepts: User Interface, TERA Recommendation Model, & APIs.
The TERA Memo UI is a React Micro FrontEnd (MFE) that communicates with the TERA Memo API and the existing Claim Evidence API.
TERA Recommendation model runs nightly to abstract relevant information and input recommendations in the VBMS Core database for each
question on the TERA Memorandum Form based on available data in a Veteran's Claim Evidence.
The respective APIs then integrate with an Oracle DB for data retrieval.  The database is populated by AI model outputs from AWS SageMaker
with use of AWS Comprehend.
Systems Interface Description (SV-1)
The SV-1 provides information about the composition and interaction of Systems. Each system involved in the architecture should be represented,
showing the VASI ID in the << >> Stereotype. Interfaces between systems must be displayed as lollipop notation, where the service provider has the API
/Service shown as the lollipop and service consumers "eating" the lollipop. Dependencies or other relationships can also be shown as arrows as
appropriate.


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Operational Resource Flow (OV-2): Data flow showing interactions between 7 systems - SageMaker querying OpenSearch, Claims API pulling from VBMS DB, UI accessing evidence, and DocGen uploading to eFolder

![Operational Resource Flow (OV-2): Data flow showing interactions between 7 systems - SageMaker querying OpenSearch, Claims API pulling from VBMS DB, UI accessing evidence, and DocGen uploading to eFolder](docs/images/page_8_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-9"></a>

## Page 9

Gray Rectangle = External VBMS resource to resource being documented
White Rectangle = Internal VBMS resource to resource being documented
Component References Table
Name
Description
Ports
Protocols
CPUI
#3028
Houses bip-cpui-tera-memo-ui TERA Memorandum Form
443
https
AWS
SageMak
er
Builds and deploys models that store auto-population data output into VBMS Core Database
443
https
ILER API
#3004
The ILER API is a service used to automate the upload process of ILER IES records into the VBMS eFolder. This functionality will
allow the seamless integration and transfer of the Service member/Veteran's ILER IES record into VBMS. By replacing the current
manual process, this service will minimize the opportunity for human error as well as the possibility of duplicate efforts.
443
https
VBMS
#1728
VBMS Core Database (Model Output from AWS SageMaker via ML-MATS & Metric of Submitted data)
443
https
DocGen
Genstore
API
#3000
Support creation & submission of PDF documents
443
https
BIA
Claims
API
#3237
Claims API retrieves Veteran's Claim data to support ability to associate the TERA Memorandum to appropriate open claims
during the Submit TERA Memorandum process.
443
https
CFAPI
Veteran
API
#3004
Provides the current Veteran's Name and File number to populate the TERA Memorandum Form Veteran Details.
443
https
Claim
Evidence
API
#3023
On Preview, DocGen API generates a PDF document including the generation of a Document ID and then DocGen API has a
follow-on request to show the generated document the with equivalent fields representing the completed digital TERA
Memorandum form in a new browser tab.
On Submit, DocGen API generates a PDF and uploads to the Veteran's Claim Evidence (eFolder).
443
https
Services Context (SvcV-1) (VASI
)
APIs


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Systems Interface Description (SV-1): UML component diagram using lollipop notation showing TERA Memo UI (CPUI #3028) with required interfaces to Claims Evidence, Claims, ILER, Veteran, and DocGen APIs, all via HTTPS port 443

![Systems Interface Description (SV-1): UML component diagram using lollipop notation showing TERA Memo UI (CPUI #3028) with required interfaces to Claims Evidence, Claims, ILER, Veteran, and DocGen APIs, all via HTTPS port 443](docs/images/page_9_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-10"></a>

## Page 10

The Svc-V1 Service Context's purpose is to describe and identify service composition and interaction. It shows a given Application Component, its services
(SOAP, REST, RPC, EJB, Messaging), and its immediate service dependencies. The context for this diagram shows several elements:
Service
/API
Operation
ID
Description
Claims
Evidence
(CE) API
On Auto-Population, CE API retrieves information from VBMS database table of TERA recommendations
(OCR_TEXTRACT_DATA) to auto-populate the TERA Memorandum form and retrieve relevant documents for including in
links to specific evidence locations supporting manual review.
Leveraging CE API with annotations/custom viewer to link directly to specific text within a document.
On Submission of TERA Memorandum form, CE API will write metrics of submitted answers to database table (VBMSUI.
TERAMEMOUPLOADMETRICS).
Claims
API
Claims API retrieves Veteran's Claim data to support ability to associate the TERA Memorandum to appropriate open
claims during the Submit TERA Memorandum process.
DocGen
Genstore
API
On Preview, DocGen API generates a PDF document including the generation of a Document ID and then DocGen API
has a follow-on request to show the generated document the with equivalent fields representing the completed digital
TERA Memorandum form in a new browser tab.
On Submit, DocGen API generates a PDF and uploads to the Veteran's Claim Evidence (eFolder).
Veteran
API
Called to get the current Veteran's Name and File number to populate the TERA Memorandum Form Veteran Details.
ILER API
Called to retrieve Veteran's ILER IES record to support auto-population of question 2.
Services Resource Flow (SvcV-2)
A SvcV-2 specifies the Resource Flows between Services and may also list the protocol stacks used in connections. Its purpose is to give a precise
specification of a connection between Services, showing specific resource operation dependencies.


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Services Context (SvcV-1): Service composition showing API operations - Claims Evidence API (get recommendations, annotations, write metrics), DocGen API (generate PDF, upload), Claims API (get claims), ILER API (get exposure records)

![Services Context (SvcV-1): Service composition showing API operations - Claims Evidence API (get recommendations, annotations, write metrics), DocGen API (generate PDF, upload), Claims API (get claims), ILER API (get exposure records)](docs/images/page_10_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-11"></a>

## Page 11

Source System
Source Service
Source Operation
Target System
Target Service
Target Operation
TERA Memo UI
 Veteran API Resource
 getVeteran
 CFAPI
 Veteran API Service
 findVeteran
TERA Memo UI
 ILER API Resource
requestIlerDocument


TERA Memo UI
 TeraMemoController
 getTeraMemoData

 Claimant Service
 retrieveFlashes
TERA Memo UI
 TeraMemoController
 postTeraMemoMetrics



TERA Memo UI
 FileController
 getData



TERA Memo UI
 Claims Resource
 getClaimsByVeteran



TERA Memo UI
GenstoreFeignClientOther
generateDocument



Internal and External Systems-Systems Matrix (SV-3/SvcV-3) (VASI Interfaces)
System/Service A
Service / System B
Internal or External
Consumer or Dependency (in relation to System A)
Claim Evidence: CE API (3023)
CPUI: TERA Memo UI (3028)
Internal VBMS
Dependency
BIA Benefits Services: Claims API (3232)
CPUI: TERA Memo UI (3028)
Internal VA
Dependency
DocGen: Genstore API (3000)
CPUI: TERA Memo UI (3028)
Internal VBMS
Dependency
CFAPI: Veteran API (3004)
CPUI: TERA Memo UI (3028)
Internal VBMS
Dependency
CFAPI: ILER API (3004)
Claim Evidence: CE API (3023)
Internal VBMS
Consumer
CPUI: MFE Auth Util (3028)
CPUI: TERA Memo UI (3028)
Internal VBMS
Dependency
State Transitions (OV-6b)
The OV-6b's purpose is to indicate how the status of key objects change in response to activities in the system. It shows how resources change over time.
Any object that has a discrete set of statuses or a lifecycle requires a state-transition diagram.


---

<a name="page-12"></a>

## Page 12: Conceptual Data Viewpoint Model (DIV-1)


Data Models
Conceptual Data Viewpoint Model (DIV-1)
Logical Data Viewpoint Model (DIV-2)


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Conceptual Data Model (DIV-1): Entity-Relationship Diagram with 5 entities - TERA_MEMO, TERA_QUESTION_ANSWER, EVIDENCE_LINK, OCR_TEXTRACT_DATA, TERA_RECOMMENDATION - showing 1:N relationships

![Conceptual Data Model (DIV-1): Entity-Relationship Diagram with 5 entities - TERA_MEMO, TERA_QUESTION_ANSWER, EVIDENCE_LINK, OCR_TEXTRACT_DATA, TERA_RECOMMENDATION - showing 1:N relationships](docs/images/page_12_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


**Diagram 2**:


**Diagram Description**: Logical Data Flow: Six-stage flow from Document Upload → OCR Processing → OpenSearch Indexing → AI Model Execution → UI Retrieval → Submission with PDF generation

![Logical Data Flow: Six-stage flow from Document Upload → OCR Processing → OpenSearch Indexing → AI Model Execution → UI Retrieval → Submission with PDF generation](docs/images/page_12_diagram_2.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-13"></a>

## Page 13: Physical Data Viewpoint Model (DIV-3)

Physical Data Viewpoint Model (DIV-3)


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Physical Data Model (DIV-3): Oracle database schema showing two main tables - OCR_TEXTRACT_DATA (with columns for each question's AI answers, confidence scores, evidence JSON) and TERAMEMOUPLOADMETRICS (tracking VSR submissions and model performance)

![Physical Data Model (DIV-3): Oracle database schema showing two main tables - OCR_TEXTRACT_DATA (with columns for each question's AI answers, confidence scores, evidence JSON) and TERAMEMOUPLOADMETRICS (tracking VSR submissions and model performance)](docs/images/page_13_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-14"></a>

## Page 14

Process View (Business Process Model)
)
Main Business Process Model (OV-6d


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Business Process Model (OV-6d): Two-phase deployment showing Phase 1 Nightly Batch (9 steps from document identification to model execution) and Phase 2 VSR Interactive (13 steps from login to TERA completion)

![Business Process Model (OV-6d): Two-phase deployment showing Phase 1 Nightly Batch (9 steps from document identification to model execution) and Phase 2 VSR Interactive (13 steps from login to TERA completion)](docs/images/page_14_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-15"></a>

## Page 15

Process Sequence - Systems Event-Trace Description (SV-10c)
The below diagram outlines the interactions between functional resources.


### Diagrams and Figures

**Diagram 1**:


**Diagram Description**: Process Sequence Event Trace (SV-10c): Sequence diagram with 20+ interactions between VSR, TERA UI, Claims Evidence API, VBMS DB, DocGen API, and eFolder showing complete auto-populate and submit flow with timing (500ms queries, 2-3sec PDF gen)

![Process Sequence Event Trace (SV-10c): Sequence diagram with 20+ interactions between VSR, TERA UI, Claims Evidence API, VBMS DB, DocGen API, and eFolder showing complete auto-populate and submit flow with timing (500ms queries, 2-3sec PDF gen)](docs/images/page_15_diagram_1.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


**Diagram 2**:


**Diagram Description**: Feature Flag Configuration: Decision tree with master flag TERA_MEMO_ENABLED branching to MODERNIZED_FORM, AUTO_POPULATE (with sub-flags for questions 1,3,4,6), METRICS, ANNOTATOR_VIEW, and multipleHighlights flags

![Feature Flag Configuration: Decision tree with master flag TERA_MEMO_ENABLED branching to MODERNIZED_FORM, AUTO_POPULATE (with sub-flags for questions 1,3,4,6), METRICS, ANNOTATOR_VIEW, and multipleHighlights flags](docs/images/page_15_diagram_2.png)

<details>
<summary>📊 View detailed text description of this diagram</summary>

For a complete textual description of this diagram that GitHub Copilot can understand, see the [DIAGRAMS_DESCRIBED.md](./DIAGRAMS_DESCRIBED.md) file.

</details>


---

<a name="page-16"></a>

## Page 16

Implementation View
Primary System Technologies (SV-9) (VASI Technology Components)
For standard tools see VBMS SV-9 Master Table.
Software Type
Software Vendor
Software Name
Software Version
TRM Link
TRM ID
Development Tool
OpenJS Foundation
Node.js
Latest
Link
6716
Cloud Services/Server Virtualization
Amazon
Sagemaker
N/A
N/A
N/A
Cloud Services/Server Virtualization
Amazon
Comprehend
N/A
N/A
N/A
Development Tool
Python Software Foundation
Python
Latest
Link
5702
Deployment View
Environment Mapping
See VBMS Environments Info Page for a current list of environments and descriptions. TERA Memo UI is deployed to all VBMS environments.
System Configuration
Feature Flag
Purpose
Location (Github)
TERA Memorandum
Form
Enables ability to toggle on / off the TERA Memorandum Form from VBMS Claim Evidence.
vbms.ui.veteran.
enableTeraMemo
Auto-Population
Button
Enables ability to toggle on / off the Auto-Population capability from the TERA Memorandum
Form for question 1,2A,3,4,6.
AUTO_POPULATE_ENAB
LED
TERA Metric
Gathering
Enables ability to toggle on / off the TERA Memorandum Form metric gathering to database.
METRICS_ENABLED
TERA Legacy
Enables ability to show the TERA Memo MFE in place of the legacy version of the page.
vbms.ui.mfeAdapter.
teraMemo.enabled
TERA Auto-populate
Metric Gathering
Enables ability to toggle on / off the TERA Memorandum Form metric gathering for auto-populate
responses to database.
WRITE_AUTO_POP_TRA
CKING_FIELDS
TERA Memo 2A
Auto-Population
Enables ability to toggle on / off the Auto-Population capability for TERA Memorandum form
question 2A.
AUTO_POPULATE_2A_EN
ABLED
TERA Memo 6 Auto-
Population
Enables ability to toggle on / off the Auto-Population capability for TERA Memorandum form
question 6.
AUTO_POPULATE_6_ENA
BLED
Annotator Document
Viewer
Enables ability to use annotator document viewer in VBMS.
OPEN_EVIDENCE_DOCS
_IN_ANNOTATOR_VIEW
Return EDIPI
Returns EDIPI from Veteran API
GET_EDIPI_ENABLED
ILER Call
Enables ILER call from CE API
tera.memo.iler.enabled
TERA Auto-
Populated Question
Indicators
Defines which questions display the AI-generated hint text in the TERA Memorandum Form UI,
indicating they may be auto-filled based on available evidence.
AUTO_POPULATED_QUE
STIONS_IDS
TERA Multiple
Highlights
Enables the ability to handle multiple highlights per supporting document in the TERA
Memorandum Form instead of a single highlight per document in VBMS Claim Evidence API.
tera.memo.data.enabled
TERA Memo Data
Enables the ability to toggle on / off the TERA Memorandum Form auto-population capability and
all related functionality in VBMS Claim Evidence API.
tera.memo.
multipleHighlights.enabled
Last Updated:

30 Jul 2025


---

<a name="page-17"></a>

## Page 17

Key
Properties
Purpose
Location (Github)
TERA Import
URL - MFE
The import URL for the TERA
Memo MFE.
vbms.ui.mfeAdapter.teraMemo.import
CE_URL
The URL for Claim Evidence API.
https://github.com/department-of-veterans-affairs/bip-cpui-config
CLAIMS_URL
The URL for Claims API.
https://github.com/department-of-veterans-affairs/bip-cpui-config
VET_URL
The URL for Veteran API.
https://github.com/department-of-veterans-affairs/bip-cpui-config
DOCGEN_URL
The URL for DocGen Genstore API.
https://github.com/department-of-veterans-affairs/bip-cpui-config
VEFS_CE_URL
The URL for opening document
links in a separate tab.
https://github.com/department-of-veterans-affairs/bip-cpui-config/blob/development/charts/bip-
cpui-tera-memo-ui/dev/values-dev.yaml#L36
System Monitoring and Metrics
The ML-MATS Platform provides system monitoring and metrics for TERA Memorandum in the below dashboard:
Monitoring and Dashboards
System Logging and Auditing
Audits follow standard BIP Platform Auditing practices.
Security Strategy
Security follows standard BIP Platform Security practices.
Compliance Scanning
Aligned with VBMS Resiliency Team regarding required security scanning standards on BIP Platform.
CodeQL
PrismaCloud
Rollback Procedures
In the case of a deployment related issue that is unable to be fixed within a given maintenance window, TERA Automation ART
will revert to previous working versions and leverage feature flags accordingly.
Backup Strategy
Assets
All development code is stored in Github and version controlled.
All data is stored within the respective environment VBMS database tables that have their appropriate backup
strategies in place.
In the case of issues with the TERA Memorandum Form
UI Issues will result in a feature flag of the entire form toggled off from VBMS with a communication from VA
Leadership to end users on instructions to leverage manual PDF provided by VBA & Compensation Services.
Auto-Population issues will result in a feature flag toggled off for the Auto-Population Button along with communication
to end users to continue use of the digital TERA Memorandum form on VBMS without auto-population functionality by
VBA & Compensation Services.
In the case of BIP Platform infrastructure downtime, we will coordinate with both BIP Platform System Team & VBMS System
Team to re-enable the TERA Memorandum form accordingly.
TERA Memo Permissions
Permissions for accessing TERA Memorandum Form in VBMS have been granted based on users having the permissions to upload
documents.
Users without proper permissions are unable to view the "TERA Memo" button in the actions dropdown of the Veteran profile
page.
Users without proper permissions are unable to access the TERA Memorandum Form via direct URL.


---

