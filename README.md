# CE-RISE Product Profile

[![Schemas](https://img.shields.io/badge/Generated%20Schema%20Files-JSON%2C%20SHACL%2C%20OWL-32CD32)](https://ce-rise-models.codeberg.page/product-profile/)


This repository provides the core data model defining the mandatory Product Profile for any Digital Product Passport, including product attributes, manufacturer details, and traceability information.

---

## Repository structure

```
/
├─ model/          # LinkML source files (.yaml)
├─ profiles/       # composition YAMLs combining modules
├─ mappings/       # SSSOM and JSON-LD mappings
├─ generated/      # auto-generated JSON Schema, SHACL, OWL
├─ samples/        # example data instances
├─ tests/          # validation tests
└─ README.md
```

---

## Data Model Structure

The Product Profile data model is structured as a hierarchical taxonomy defining mandatory information for Digital Product Passports. The model is built using [LinkML](https://linkml.io/) and generates multiple schema formats (JSON Schema, SHACL, OWL).

### Core Hierarchy

```
ProductIdentification (root)
├── 1. GeneralProductInformation
│   ├── LotBatchNumber
│   ├── GTIN14
│   ├── SerialNumber
│   └── UniqueProductIdentifier
├── 2. ManufacturersInformation
│   ├── CompanyId
│   ├── Name
│   ├── ManufacturingDate
│   ├── PostalAddress
│   ├── RegisteredTradeNameOrTradeMark
│   ├── UniqueFacilityIdentifiers
│   ├── UniqueOperatorIdentifier
│   └── Website
├── 3. InformationRelatedToTheImporter
│   └── EoriNumber
├── 4. ProductTraceability
│   ├── Date
│   ├── LocationUniqueFacilityIdentifiers
│   └── OperatorsUniqueOperatorIdentifier
├── 5. ProductSpecification
│   ├── ProductCostAndPricing
│   └── WeightAndVolumeOfTheProductAndItsPackaging
└── 6. SpecificProductInformation
```

### Workflow Sequence

#### **Step 1: GeneralProductInformation** 
Basic product identification with multiple identifier types:
- **LotBatchNumber**: Lot/batch tracking information
- **GTIN14**: Global Trade Item Number (14-digit format with GS1 integration)
- **SerialNumber**: Individual product serial numbers
- **UniqueProductIdentifier**: Enables web link to product passport

#### **Step 2: ManufacturersInformation**
Manufacturer details - Contains manufacturer-related classes:
- **CompanyId**: Various ID formats (GS1 GLN, IEC 61406, SKU ID, etc.)
- **Name**: Manufacturer's legal name (Art 21 6. ESPR)
- **ManufacturingDate**: Month/year in manufacturing date codes
- **PostalAddress**: Physical address (Art 21 6. ESPR)
- **RegisteredTradeNameOrTradeMark**: Registered business names and trademarks
- **UniqueFacilityIdentifiers**: Value chain location identifiers
- **UniqueOperatorIdentifier**: Value chain actor identifiers
- **Website**: Manufacturer's website

#### **Step 3: InformationRelatedToTheImporter**
Import/export details - Contains the EoriNumber class

#### **Step 4: ProductTraceability**
Supply chain tracking - Contains Date, LocationUniqueFacilityIdentifiers, and OperatorsUniqueOperatorIdentifier classes

#### **Step 5: ProductSpecification**
Technical specifications - Contains ProductCostAndPricing and WeightAndVolumeOfTheProductAndItsPackaging classes

#### **Step 6: SpecificProductInformation**
Additional product-specific information

### Data Properties

Each class has a corresponding value property (e.g., `name_value`, `company_id_value`) that holds the actual data. All value properties are string type except where specified otherwise.


---

## Development Roadmap

...


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
