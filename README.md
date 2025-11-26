# CE-RISE Product Profile

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17723238.svg)](https://doi.org/10.5281/zenodo.17723238) [![Schemas](https://img.shields.io/badge/Generated%20Schema%20Files-JSON%2C%20SHACL%2C%20OWL-32CD32)](https://ce-rise-models.codeberg.page/product-profile/)


This repository provides the core data model defining the mandatory Product Profile for any Digital Product Passport, including product attributes, manufacturer details, and traceability information.

---

## Repository structure

```
/
├─ model/          # LinkML source files (.yaml): required
├─ mappings/       # SSSOM and JSON-LD mappings: optional
├─ generated/      # locally generated JSON Schema, SHACL, OWL: optional - CI/CD deploys on pages
├─ samples/        # example data instances: optional
├─ tests/          # validation tests: optional
└─ README.md       # required
```

---

## Data Model Structure

The Product Profile data model is structured as a hierarchical taxonomy defining **static foundational information** for Digital Product Passports. The model captures product identity and origin data that remains constant throughout the product lifecycle. Built using [LinkML](https://linkml.io/), it generates multiple schema formats (JSON Schema, SHACL, OWL).

**Core Philosophy**: This model answers fundamental questions about product identity:
- **"What is this product?"** → Product identification and classification
- **"Who made it and where?"** → Manufacturing origin and facility details  
- **"How did it get here?"** → Import/export compliance and customs
- **"What is it made of?"** → Basic materials and physical properties

Dynamic supply chain events, lifecycle tracking, and real-time traceability are addressed by separate, complementary data models.

### Core Hierarchy

```
ProductIdentification (root)
├── 1. GeneralProductInformation
│   ├── LotBatchNumber
│   ├── GTIN14
│   ├── SerialNumber
│   ├── ProductImages
│   ├── ProductType
│   └── UniqueProductIdentifier
├── 2. ManufacturersInformation
│   ├── OrganizationEntity (GS1 GLN, LEI, VAT, legal name)
│   ├── ManufacturingFacility (facility GLN, OSID, coordinates)
│   ├── Name
│   ├── ManufacturingDate
│   ├── PostalAddress
│   ├── RegisteredTradeNameOrTradeMark
│   ├── UniqueFacilityIdentifiers
│   ├── UniqueOperatorIdentifier
│   └── Website
├── 3. InformationRelatedToTheImporter
│   ├── EoriNumber (validated format: 2-letter country + up to 15 alphanumeric)
│   ├── CustomsDocumentation (MRN, declaration IDs, authorities, document URLs)
│   ├── ImportExportOperation (trade operations with Incoterms, values, dates)
│   ├── ImporterJurisdiction (EU 3-character country codes)
│   ├── TariffClassification (HS, CN, TARIC codes with duty rates)
│   ├── BorderCrossing (UN/LOCODE port codes, customs offices, crossing dates)
│   ├── AEOStatus (Authorized Economic Operator certification)
│   └── ImportAuthorization (licenses and permits for restricted goods)
└── 4. ProductSpecification
    ├── WeightAndVolumeOfTheProductAndItsPackaging
    └── BasicMaterials (simple material names)
```

### Workflow Sequence

#### **Step 1: GeneralProductInformation** 
Basic product identification with multiple identifier types:
- **LotBatchNumber**: Lot/batch tracking information
- **GTIN14**: Global Trade Item Number (14-digit format with GS1 integration)
- **SerialNumber**: Individual product serial numbers
- **ProductImages**: Product images for branding/visual identification (comma-separated URLs)
- **ProductType**: Product classification (3-digit GTIN prefix or alphanumeric code)
- **UniqueProductIdentifier**: Enables web link to product passport

#### **Step 2: ManufacturersInformation**
Manufacturer details with GS1-centric hierarchical structure:
- **OrganizationEntity**: Legal entity with GS1 GLN (preferred), LEI code, VAT number, company registration
- **ManufacturingFacility**: Physical facilities with facility GLN, Open Supply Hub ID, GPS coordinates

- **Name**: Manufacturer's legal name (Art 21 6. ESPR)
- **ManufacturingDate**: Month/year in manufacturing date codes
- **PostalAddress**: Physical address (Art 21 6. ESPR)
- **RegisteredTradeNameOrTradeMark**: Registered business names and trademarks
- **UniqueFacilityIdentifiers**: Value chain location identifiers
- **UniqueOperatorIdentifier**: Value chain actor identifiers
- **Website**: Manufacturer's website

#### **Step 3: InformationRelatedToTheImporter**
Comprehensive import/export tracking and compliance with EU customs regulations:
- **EoriNumber**: EU registration number with validated format (2-letter country code + up to 15 alphanumeric chars, e.g., GB123456789000)
- **CustomsDocumentation**: Customs documents (MRN, declaration IDs) with issuing authorities and digital document URLs (PDF/DOC/images)
- **ImportExportOperation**: Trade operations with type validation (IMPORT/EXPORT/TRANSIT/RE_EXPORT), dates, shipment IDs, quantities, Incoterms (FOB/CIF/EXW/DDP), and monetary values with currency codes
- **ImporterJurisdiction**: Legal establishment country using EU Publications Office 3-character country codes for EORI validation
- **TariffClassification**: International trade classification with 6-digit HS codes, 8-digit EU CN codes, 10-digit TARIC codes, descriptions, and duty rates
- **BorderCrossing**: Border crossing tracking with UN/LOCODE port codes (e.g., DEHAM, NLRTM), customs office codes, and precise crossing timestamps
- **AEOStatus**: Authorized Economic Operator certification (AEOC/AEOS/AEOF) for trusted trader benefits and trade facilitation
- **ImportAuthorization**: Import licenses and permits for restricted goods with validity periods and issuing authorities

#### **Step 4: ProductSpecification**
Essential physical and material information:
- **WeightAndVolumeOfTheProductAndItsPackaging**: Physical dimensions and packaging details
- **BasicMaterials**: Simple material names for basic composition identification

### Data Properties

Each class has a corresponding value property (e.g., `name_value`, `company_id_value`) that holds the actual data. All value properties are string type except where specified otherwise.


---

## Development Roadmap

| Step | Component | Criticalities Identified | Solutions Implemented | Status | Missing/TODO |
|------|-----------|-------------------------|----------------------|--------|--------------|
| **1** | **GeneralProductInformation** | • Unique product identifier lacks precision and standards<br>• No reference integration with discoverability/registries<br>• Missing serial number and lot number storage<br>• No connection to standard product nomenclature<br>• No product description and branding<br>• No classification for grouping products | • Added GS1 prefix and ontology integration<br>• Implemented GTIN-14 + serial number approach<br>• Added Schema.org prefix<br>• Created GTIN-14, Serial number, Lot/batch number subclasses<br>• Added ProductImages (comma-separated image URLs with format validation)<br>• Added ProductType (3-digit GTIN prefix or alphanumeric classification)<br>• Referenced UNTP framework for discoverability | **COMPLETED** | • UNTP Identity Resolver integration |
| **2** | **ManufacturersInformation** | • Incomplete description and separation of manufacturer facility and organization<br>• Lack of codification of facility and organization | • Implemented GS1-centric hierarchical model<br>• Added OrganizationEntity with GLN, LEI, VAT identification<br>• Added ManufacturingFacility with facility GLN and OSID<br>• Added GPS coordinates for precise facility location<br>• Renamed 'Company ID' to 'Organization identifier'<br>• Renamed 'Unique facility identifiers' to 'Facility identifier'<br>• Renamed 'Unique operator identifier' to 'Operator identifier' | **COMPLETED** | • GS1 GLN Registry integration<br>• Open Supply Hub API integration<br>• LEI code verification integration |
| **3** | **InformationRelatedToTheImporter** | • Limited to EORI number only<br>• Missing comprehensive import/export tracking<br>• No customs documentation integration<br>• No tariff classification system<br>• Missing border crossing information | • EORI number with validated EU format (2-letter country + alphanumeric)<br>• CustomsDocumentation with MRN, declaration IDs, and document URLs<br>• ImportExportOperation with trade activity tracking and Incoterms<br>• ImporterJurisdiction with EU 3-character country codes<br>• TariffClassification with HS/CN/TARIC codes and duty rates<br>• BorderCrossing with UN/LOCODE port codes and customs offices<br>• AEOStatus for trusted trader certification<br>• ImportAuthorization for restricted goods licensing | **COMPLETED** | • Real-time customs status API integration<br>• Tariff database integration (WTO, EU TARIC)<br>• Multi-modal transport tracking<br>• Trade compliance validation engines |
| **4** | **ProductSpecification** | • Limited to physical dimensions only<br>• Missing basic material information | • WeightAndVolumeOfTheProductAndItsPackaging for physical attributes<br>• BasicMaterials for simple material identification<br>• Focused on essential product characteristics | **NEEDS SPECIFICATION** | • Material dictionary/nomenclature standard (ISO, UNSPSC, etc.)<br>• Physical attribute measurement standards<br>• Enhanced dimensional specifications<br>• Regulatory compliance alignment |

### Development Priorities

**Current Status:** Steps 1-3 are **COMPLETED**, Step 4 needs specification work:
- **Steps 1-3**: Complete product identification, manufacturer details, and import/export compliance
- **Step 4**: Basic structure in place but requires specification standards
- **Integration Focus**: GS1 Registry, Open Supply Hub, customs authorities, TARIC database integration
- **Enhancement Opportunities**: Enhanced precision, material standards, and system integrations

**Next Phase Focus:** Complete specification work for Step 4:
- **Step 4**: Establish material dictionary and physical attribute measurement standards

**Focused Product Profile Scope:** The model provides essential information to answer:
- **"What is this product?"** (identification, classification, physical attributes)
- **"Who made it and where?"** (manufacturer, facility, certification details)  
- **"How did it get here?"** (import/export, customs, compliance)

- **"What is it made of?"** (basic materials and physical properties)

**Implementation Dependencies:**
- **GS1 Registry Integration**: GLN verification and lookup services
- **Open Supply Hub API**: Facility verification and OSID integration  
- **LEI Registry**: Legal Entity Identifier verification
- **Customs Integration**: Real-time EORI validation and customs status
- **TARIC Database**: Tariff classification validation and duty calculation
- **UNTP Framework**: Product discoverability and identity resolution

**Complementary Data Models** (Outside Product Profile Scope):
- **Dynamic Traceability Model**: Real-time supply chain events, lifecycle tracking, ownership changes
- **Product Specifications Model**: Detailed material composition, performance metrics, quality data
- **DPP System Infrastructure Model**: Data carriers, access control, APIs, interoperability
- **Commercial Information Model**: Pricing, costs, commercial terms, market data


---

## Publishing

Release artifacts for each version (`schema.json`, `shacl.ttl`, `model.owl`)  
are served directly from this URL:
```
https://ce-rise-models.codeberg.page/product-profile/
```

---

## Accessing Previous Releases

If you want to view the files published for version `v1.2.0`, open:

```
https://codeberg.org/CE-RISE-models/product-profile/src/tag/pages-v1.2.0/generated/
```

Files available in that directory typically include:

- schema.json
- shacl.ttl
- model.ttl
- index.html



---
<a href="https://europa.eu" target="_blank" rel="noopener noreferrer">
  <img src="https://ce-rise.eu/wp-content/uploads/2023/01/EN-Funded-by-the-EU-PANTONE-e1663585234561-1-1.png" alt="EU emblem" width="200"/>
</a>

Funded by the European Union under Grant Agreement No. 101092281 — CE-RISE.  
Views and opinions expressed are those of the author(s) only and do not necessarily reflect those of the European Union or the granting authority (HADEA).  
Neither the European Union nor the granting authority can be held responsible for them.

© 2025 CE-RISE consortium.  
Licensed under [Creative Commons Attribution–NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).  
Attribution: CE-RISE project (Grant Agreement No. 101092281) and the individual authors/partners as indicated.

<a href="https://www.nilu.com" target="_blank" rel="noopener noreferrer">
  <img src="https://nilu.no/wp-content/uploads/2023/12/nilu-logo-seagreen-rgb-300px.png" alt="NILU logo" width="40"/>
</a>

Developed by NILU (Riccardo Boero, Mahsa Motevallian) within the CE-RISE project.
