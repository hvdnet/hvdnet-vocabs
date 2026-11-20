# 🤖 Agent Intelligence & Project Guidance

Welcome, Agent. This document provides essential context and instructions for working on the **HVDNet Vocabularies** (`hvdnet-vocabs`) repository. Follow these guidelines to ensure consistency, quality, and semantic rigor across all vocabularies.

---

## 🚀 Project Overview & Objectives

HVDNet Vocabularies is developed and maintained by the [High-Value Data Network](https://highvaluedata.net). The project provides controlled sets of concepts, statistical metrics, and data quality measures modeled in **W3C SKOS** (Simple Knowledge Organization System) for FAIR data stewardship, metadata profiling, and cross-tool interoperability.

### Published Vocabularies
1. **Descriptive Statistics Vocabulary (`statistics.ttl`)**: A generic, tool-agnostic taxonomy of summary statistics, distribution properties, robust location/scale metrics, and data quality indicators for FAIR data.
2. **QSV Vocabulary (`qsv-statistics.ttl`)**: Controlled vocabulary covering statistical measures and data profiling metrics produced by the `qsv stats` and `qsv moarstats` commands from the [QSV Data Wrangling package](https://qsv.dathere.com/), mapped to `statistics.ttl`.

### Publishing Platform
Vocabularies are published using a **[Skosmos](https://skosmos.org/)** vocabulary browser server backed by a SPARQL triple store (e.g., Apache Jena Fuseki).

---

## 🛠 Tech Stack & Standards

- **Serialization**: W3C Turtle RDF (`.ttl`)
- **Knowledge Model**: W3C SKOS Core, Dublin Core Terms (`dct:`), RDFS, XSD
- **Interoperability Crosswalks**: Wikidata, DDI Alliance Controlled Vocabularies (`ddi:`)
- **Custom Properties**:
  - `statscv:formula`: LaTeX mathematical formula describing the computation.
  - `statscv:computationMethod`: Textual, step-by-step computation instructions.
- **Licensing**:
  - **Vocabularies & Documentation**: Creative Commons Attribution 4.0 International ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
  - **Software, Scripts, & Tooling**: [MIT License](LICENSE).

---

## 📂 Project Structure

- `statistics.ttl`: Primary descriptive statistics taxonomy.
- `qsv-statistics.ttl`: QSV command statistics mapped to SKOS concepts.
- `scripts/`: Validation scripts and SPARQL queries.
- `LICENSE`: Dual-license definition (CC BY 4.0 + MIT).
- `README.md`: Public documentation and vocabulary index.
- `AGENTS.md`: Agent Intelligence & Project Guidance.

---

## 📖 SKOS Authoring Conventions & Skosmos Readiness

### 1. Concept Scheme Declarations
Every `.ttl` vocabulary must define its `skos:ConceptScheme`:
```turtle
<scheme:> a skos:ConceptScheme ;
    dct:title "Vocabulary Title [DRAFT]"@en ;
    rdfs:label "Vocabulary Title [DRAFT]"@en ;
    dct:description "Detailed description..."@en ;
    dct:created "YYYY-MM-DD"^^xsd:date ;
    dct:modified "YYYY-MM-DD"^^xsd:date ;
    skos:hasTopConcept <scheme:TopConcept1>, <scheme:TopConcept2> ;
    dct:license <https://creativecommons.org/licenses/by/4.0/> .
```

### 2. Top-Level Category Concepts (Skosmos Hierarchy)
Skosmos builds its tree hierarchy using explicit top concept relations. Without full inference enabled in the triple store, top concepts **must** declare `skos:topConceptOf`:
```turtle
<scheme:TopConcept1> a skos:Concept ;
    skos:prefLabel "Category Name"@en ;
    skos:topConceptOf <scheme:> ;
    skos:inScheme <scheme:> ;
    skos:narrower <scheme:concept1>, <scheme:concept2> .
```

### 3. Leaf Concepts
Each individual concept must follow this structure:
```turtle
<scheme:myConcept> a skos:Concept ;
    skos:prefLabel "preferred label"@en ;
    skos:altLabel "alternative label"@en ;      # Optional
    skos:inScheme <scheme:> ;
    skos:broader <scheme:TopConcept1> ;
    skos:definition "Clear, concise definition."@en ;
    skos:scopeNote "Computation guidance..."@en ; # Optional
    statscv:formula "$\\bar{x} = ...$" ;         # Optional
    statscv:computationMethod "Steps..."@en ;   # Optional
    skos:exactMatch <target:Concept> .           # Optional (crosswalks)
```

---

## 🧠 Agent Guidelines & Quality Gates

1. **Reciprocal Hierarchy**: Always maintain exact bidirectional symmetry between `skos:broader` and `skos:narrower`. If a concept lists a parent in `skos:broader`, the parent's `skos:narrower` must include the concept.
2. **Alphabetical Sorting**: Maintain clean, alphabetically sorted lists for all `skos:narrower` blocks.
3. **Generic vs. Tool-Specific**:
   - `statistics.ttl` must remain generic, standardized, and focused on FAIR data principles. Avoid tool-specific heuristics or implementation details.
   - Tool-specific implementations, CLI options, and specialized flags belong in tool vocabularies (e.g., `qsv-statistics.ttl`), linked back to `statistics.ttl` via `skos:exactMatch`, `skos:closeMatch`, or `skos:broadMatch`.
4. **Validation Before Merge**:
   Always validate `.ttl` files using `rdflib` before finalizing turns:
   ```bash
   uv run --with rdflib python -c "
   import rdflib
   g = rdflib.Graph()
   g.parse('statistics.ttl', format='turtle')
   g.parse('qsv-statistics.ttl', format='turtle')
   print('Syntax valid!')
   "
   ```
5. **Metadata Maintenance**: Update `dct:modified` whenever modifying concepts in a vocabulary.
