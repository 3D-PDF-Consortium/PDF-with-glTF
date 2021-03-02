# Use Case: PDF and glTF for Drawingless Manufacturing 
---
## Description
Drawingless Manufacturing is a term used to describe a manufacturing process where an annotated digital three-dimensional (3D) model of a product serves as the authoritative information source for all manufacturing activities for that product. The process of annotating the 3D model (rather than a 2D drawing) is known as Model Based Definition (MBD).

A key advantage of Drawingless Manufacturing is that it replaces 2D engineering drawings. The 3D model contains all the information typically found on in an entire set of engineering drawings, including precise geometry and PMI (Product and Manufacturing Information) consisting of dimensions, tolerances, notes, surface finish, and material specifications.

Processes such as fabrication, assembly and installation, quality inspection and in-service support and maintenance require data in the engineering model and the visually equivalent PDF meets their needs. For example, a Quality inspector will verify that a product conforms to the requirements in the engineering design and thus needs access to the 3D shape, tolerances, process notes, etc. from the MBD model to perform the inspection. A PDF equivalent of the source MBD model provides this information at no or low cost on a wide variety of platforms. The author of a maintenance instruction needs to understand the engineering requirements for assembly when developing the maintenance procedure documentation. The PDF provides this information with the added benefit that it is in a form that may be directly repurposed into the maintenance documents

Users of MBD data often do not require or want the full capabilities of a 3D CAD system. A PDF file created from a 3D CAD model can support these uses while avoiding the cost and complexity of requiring a CAD system. 

Drawingless Manufacturing is an important component of the Model Based Enterprise (MBE) and has been adopted by many manufacturers around the world, in a wide range of industries including Aerospace and Defense, as well as automotive.

## Actors 
| Actor | Description |
| :---- | :---------- |
| **Engineering** | Engineers author MBD data in a CAD environment. Engineers embed tolerances and other requirements in the 3D CAD model via annotations, notes, etc. CAD based MBD data is converted to PDF to facilitate use by downstream users. |
| **Manufacturing and Quality** | Manufacturing refers to the engineering requirements in the 3D MBD data during part planning, manufacturing and assembly. Quality organizations ensure that the manufactured part conforms to the requirements in the engineering definition. |
| **Maintenance and Support** | Authors of maintenance procedures need to understand the engineering requirements to ensure that maintenance is performed correctly. The maintenance tasks will be performed across a geographically dispersed workforce, often is austere conditions and under schedule pressure. Ease of access to the MBD data and derivative maintenance documentation with minimal infrastructure requirements are keys to these processes. |
| **Regulators** | In industries that are regulated, for example commercial aviation, regulatory bodies require access to product data for review, audit and other regulatory and certification processes. Regulators typically work with multiple companies in an industry and need CAD neutral data to avoid the cost of maintaining multiple CAD environments in order to view MBD data from different companies. |


## Purpose ##
| Actor | Goal |
| :---- | :---------- |
| **MBD Data Producers** | Ensure that a lightweight PDF is equivalent in content to the source CAD model and encodes all of the required engineering information in an easy to consume format. |
| **MBD Data Consumers** | Have access to the MBD data for use in their processes with minimal hardware/software, infrastructure and training cost. Enable easy repurposing of the authored MBD data into downstream documents such as manufacturing plans, work instructions and maintenance procedure documents. The goal is to avoid the cost and complexity of requiring a CAD environment wherever the MBD data is consumed by users downstream of engineering. |

Typical course of events:
----------------------

| Actor    | Action                                                     | System Response |
| -------- | :--------------------------------------------------------- | :-------------- |
| Engineer | Authors model based definition (MBD) of part in CAD system |                 |
| Engineer | Saves/translates CAD visual data to glTF format.           |                 |
| Engineer | Saves/translates CAD geometry data to STEP format.         |                 |
| Engineer | Validates glTF and STEP data                               |                 |
| Engineer | Authors PDF from glTF and STEP data.                       |                 |
|          |                                                            |                 |

