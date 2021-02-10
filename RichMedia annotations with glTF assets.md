# RichMedia annotations with GL Transmission Format (glTF) assets

## Introduction

This document is a proposal to extend the PDF RichMedia annotation to include assets that conform to the glTF specification.

### PDF: ISO 32000

ISO 32000-2 can embed 3D CAD models as either 3D or RichMedia annotations. 3D node, stream and view dictionaries can only reference data saved in either the ECMA-363, Universal 3D (U3D) file format or ISO 14739-1, Product Representation Compact (PRC) file format. This often requires the authoritative CAD data to be translated to either U3D or PRC solely to embed the data in a PDF file.

### glTF

glTF is an API-neutral runtime asset delivery format. glTF bridges the gap between 3D content creation tools and modern 3D applications by providing an efficient, extensible, interoperable format for the transmission and loading of 3D content.

The [Khronos](https://www.khronos.org/) Group governs the glTF specification which is [published on GitHub](https://github.com/KhronosGroup/glTF).

### Extending PDF to support glTF

The purpose of this document is to extend the PDF specification to allow RichMedia annotations to include 3D assets saved in the glTF format.

## Scope

This document specifies how to extend the ISO 32000-2 specification by adding the glTF format as a valid format for 3D assets contained in a RichMedia annotation. It is intended for:

-   developers of software that creates PDF files (PDF writers);

-   software that reads existing PDF files and usually interprets their contents for display (PDF readers);

-   software that reads and displays PDF content and interacts with the computer users to possibly modify and save the PDF file (PDF processors);

-   PDF products that read and/or write PDF files for a variety of other purposes (PDF processors).

Note PDF writers and PDF readers are more specialized classifications of PDF processors.

This document does not specify the following:

-   specific processes for converting paper or electronic documents to the PDF file format;

-   specific technical design, user interface implementation, or operational details of rendering;

-   specific physical methods of storing these documents such as media and storage conditions;

-   methods for validating the conformance of PDF files or PDF processors;

-   required computer hardware and/or operating system.

## Normative references

The following documents are referred to in the text in such a way that some or all of their content constitutes requirements of this document. For dated references, only the edition cited applies. For undated references, the latest edition of the referenced document (including any amendments) applies.

*glTF*

*ISO 32000-2, Document management --- Portable Document Format --- Part 2: PDF 2.0*

## Terms and definitions

For the purposes of this document, the following terms and definitions apply.

ISO and IEC maintain terminological databases for use in standardization at the following addresses:

--- ISO Online browsing platform: available at <https://www.iso.org/obp>

--- IEC Electropedia: available at <http://www.electropedia.org/>

###  PDF (Portable Document Format)

file format defined in ISO 32000-2

###  glTF

file format defined in xxx

# RichMedia annotations with GL Transmission Format (glTF) assets

## Document Requirements

### General

Document requirements identify PDF features that are required for correct handling of a document. Requirements are stored as requirement dictionaries (see ISO 32000-2, PDF 2.0: 12.11, "Document requirement").

### Requirement types

ISO 32000-2, PDF 2.0: 12.11.2, "Requirement types" states:

*The **S** entry in a requirement dictionary identifies a feature of the PDF language or a capability that may be present in a PDF processor. Such entries enable the document to identify feature(s) of PDF beyond those commonly expected, such as 2D graphics rendering, and are required for correct handling in accordance with this standard. In addition, although not required for viewing, a document may also use requirement values that stipulate required features of PDF processors such as the ability to interact with or modify the document.*

### glTF requirement

ISO 32000-2, PDF 2.0: Table 275, "Requirement types" lists requirement types that have been defined through PDF 2.0. A new key, **glTF**, specifies that a glTF RichMedia annotation is stored in a PDF file.

**ISO 32000-2, PDF 2.0: Table 275 --- Requirement types**

| Type | Description |
|---|---|
| **glTF** | Requires support for RichMedia annotations (ISO 32000-2, PDF 2.0: 13.7.2.2, "RichMediaSettings dictionary") conforming to the ISO xxx (glTF) specification. This also includes support for associated ECMAScripts.<br />If a **V** key is present in its **Requirements** dictionary, it shall represent the version of the glTF data in the PDF file and not the PDF version. |

### Identifying glTF 3D Artwork in a requirement dictionary

PDF documents containing RichMedia annotations with assets conforming to the glTF specification shall have a Requirements dictionary containing an **S** key with the value of **glTF**.

A **V** key in a requirement dictionary is used to specify the version number for a specific technology related to the requirement in question (see ISO 32000-2, PDF 2.0: "Requirement versions").

RichMedia annotations with assets conforming to the glTF specification shall have a **V** key that specifies the version of ISO xxx used by the asset, represented as a year (decimal integer) followed by a period and a zero. For example, "2020.0".

## 3D views

### General

ISO 32000-2, PDF 2.0: 13.6.4, "3D views" states:

*A 3D view (or simply view) specifies parameters that shall be applied to the virtual camera associated with a 3D annotation.*

Named views are specified in PDF as 3D view dictionaries.

### Changes to the MS key in a 3D view dictionary

The **MS** key in a 3D view dictionaries specifies how the 3D camera-to-world transformation matrix is determined. The description of this key is modified to include the glTF format:

**ISO 32000-2, PDF 2.0: Table 315 --- Entries in a 3D view dictionary**
| **Key** | **Type** | **Description** |
|---|---|---|
| **MS** | name | (*Optional)* A name specifying how the 3D camera-to-world transformation matrix shall be determined. The following values are valid:<br /><br />*M* Indicates that the **C2W** entry shall specify the matrix<br /><br />*U3D* Indicates that the view node selected by the **U3DPath** entry in the 3D stream object shall specify the matrix.<br /><br />If omitted, the view specified in the 3D artwork shall be used.<br />NOTE 1 There is no corresponding **MS** field value ~~for the PRC file format,~~ that would correspond to a 3D stream object of type PRC or glTF. **M** is the only valid entry for 3D stream objects of type PRC or glTF (or it can be omitted). |
## 3D node dictionaries

### General

The PDF interface to 3D geometry is through 3D node dictionaries (see ISO 32000-2, PDF 2.0: 13.6.4.7, "3D node dictionaries").

### Changes to the N key in a 3D node dictionary

An **N** key in a 3D node dictionary specifies the unique name of the node being described by the node dictionary (see ISO 32000-2, PDF 2.0: Table 323, "N\"). The description of this key is modified to include the glTF format:

**ISO 32000-2, PDF 2.0: Table 323 --- Entries in a 3D node dictionary**
| **Key** | **Type** | **Description** |
|---|---|---|
| **N** | text string | (*Required)* The name of the node being described by the node dictionary. All names in the node dictionary shall be unique. Interpretation of this entry shall depend upon the 3D format specified in the **Subtype** entry in "Table 311 --- Entries in a 3D stream dictionary" as described below<br /><br />*U3D* If the **Subtype** of the corresponding 3D Stream is *U3D*, this entry shall correspond to the field Node block name, specified in the Universal 3D file format.<br /><br />*PRC* (PDF 2.0) If the **Subtype** of the corresponding 3D Stream is *PRC*, this entry shall be the unique identifier (UUID), specified in section 5.3, Unique identifiers, of ISO 14739-1.<br /><br />*glTF* If the **Subtype** of the corresponding 3D Stream is *glTF*, this entry shall be the unique identifier (UUID), specified in the glTF stream.<br /><br />NOTE 1 When comparing this entry to node names, PDF processors will need to translate between the PDF text encoding used by PDF and the character encoding specified in the 3D stream.<br/><br />NOTE 2 This description of the value of the **N** key was clarified in the 2020 dated revision of this document. |

### Creating an N key for a glTF node

If the asset of a RichMedia annotation corresponding to a 3D node dictionary is glTF, the **N** entry shall be constructed from fields stored in the glTF asset. PDF processors shall translate between the PDF text encoding used by PDF and the character encoding specified in the glTF asset.

## Marking the Extension Level in PDF

ISO 32000 defines a mechanism and process for the addition of new keys to PDF [Annex E, Extending PDF\] and a way to document their usage in a PDF [7.12.2 & 7.12.3, Extensions dictionary\].

PDF documents containing RichMedia annotations with assets conforming to the glTF specification shall have an **Extensions** dictionary that is a direct object (i.e., the information shall be nested directly within the catalog dictionary). This Extensions dictionary shall be added to an array object that is the value of the **ISO\_** key in a document\'s Extensions dictionary and adhere to the following requirements:

- The value of **BaseVersion** shall be 2.0.

- The value of **ExtensionLevel** shall be this ISO document number, xxx.

- The value of **ExtensionRevision** shall be the text string "1:2021\".

- The value of **Type** shall be DeveloperExtensions.

- The value of **URL** shall be the URL to the ISO page for this document, https://www.iso.org/standard/xxx.html.

The PDF markup for PDF documents containing RichMedia annotations with assets conforming to the glTF specification is as follows:

```
%PDF2.0
<<	/Type /Catalog
	/Extensions
	<<	/ISO
		<<	/Type /DeveloperExtensions
			/BaseVersion /2.0
			/ExtensionLevel /xxx
			/ExtensionRevision (1:2021)
			/URL (https://www.iso.org/standard/xxx.html)
		>>
	>>
>>
```