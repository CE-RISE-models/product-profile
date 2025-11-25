# CE-RISE Product Profile

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

## Generate schemas

The schemas are generated and published by the CI/CD automation. To produce the validation artifacts locally:

```bash
make all
```

This generates:
- `generated/schema.json` — JSON Schema for API validation  
- `generated/shacl.ttl` — SHACL for RDF validation  
- `generated/model.owl` — OWL ontology export  

You must commit generated files before pushing.


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
https://codeberg.org/CE-RISE-models/<repo-name>/src/tag/pages-v1.2.0/generated/
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

Developed by NILU (Riccardo Boero — ribo@nilu.no) within the CE-RISE project.  



