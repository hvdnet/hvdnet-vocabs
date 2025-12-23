# HVDNet Vocabularies – Copilot Instructions

## Project Overview

HVDNet Vocabularies hosts controlled vocabularies in **SKOS** (Simple Knowledge Organization System) format, published via **SkoHub Pages**. Currently includes the Statistics Vocabulary (`statistics.ttl`) and QSV Vocabulary (`qsv.ttl`).

## File Structure & Patterns

- **`.ttl` files** (Turtle RDF): Define concept schemes with SKOS predicates (`skos:prefLabel`, `skos:definition`, `skos:narrower`, etc.)
- **`config.yaml`**: SkoHub configuration—search attributes, UI colors, footer links
- **`statistics.ttl`**: 1183-line hierarchical taxonomy with custom properties (`stats:formula`, `stats:computationMethod`)
- **`qsv.ttl`**: QSV tool statistics mapped to SKOS concepts
- **`scripts/validate-skos`**: Bash validator using Docker + Apache Jena Fuseki + SHACL shapes
- **`.github/workflows/main.yml`**: CI/CD—triggers on TTL/YAML changes, validates & deploys via SkoHub Docker

## Key Conventions

### Turtle/SKOS Coding
- Use prefix declarations at file top: `@prefix stats:`, `@prefix skos:`, `@prefix dct:`
- Concepts are `skos:Concept` instances with:
  - `skos:prefLabel` (primary name, language-tagged)
  - `skos:topConceptOf` (for category-level concepts)
  - `skos:narrower` (broader-to-narrower relationship)
  - `skos:definition` (description)
  - `skos:scopeNote` (human-readable guidance, in stats vocabulary)
- Custom properties: `stats:formula` (LaTeX), `stats:computationMethod` (text steps)
- Interoperability: Link to external vocabularies via `skos:exactMatch` (e.g., Wikidata)

### Validation Workflow
1. Run validation locally: `./scripts/validate-skos <file.ttl>`
2. Validate with severity flags: `-l violation|warning|all`, `-o <report>` to save
3. CI auto-validates changed TTL files; stops push if violations found
4. Fuseki + SHACL shapes in `skos.shacl.ttl` enforce SKOS compliance

### Deployment
- SkoHub Docker container builds `/public` from TTL + config.yaml + static files
- Deployed to GitHub Pages on each push (via peaceiris/actions-gh-pages)
- Base URL set from repo name in `.env` 

## Common Tasks

**Add a new concept**: Define in `.ttl` with `a skos:Concept`, add `skos:prefLabel`, `skos:definition`, link via `skos:narrower` to parent.

**Update statistics vocabulary**: Add/edit concept in `statistics.ttl`, include `stats:formula` and `stats:computationMethod` where applicable, validate locally before push.

**Modify UI/search**: Edit `config.yaml` (searchableAttributes, colors, footer links), push to trigger rebuild.

**Fix validation errors**: Check SHACL report (`./scripts/validate-skos -r <file.ttl>`), ensure all required SKOS predicates present, correct syntax (Turtle prefixes, trailing periods).

## External Dependencies

- **SkoHub Pages/Docker**: Builds & publishes vocabulary site
- **Apache Jena Fuseki**: SPARQL/SHACL validation engine in Docker
- **Wikidata**: Crosswalk targets via `skos:exactMatch`
- **DDI Alliance CV**: Statistics vocabulary alignment reference

## Notes for AI Agents

- All `.ttl` files must validate without Fuseki/SHACL errors before merge
- Use existing concept definitions as templates; maintain parallel structure in concept hierarchies
- YAML config changes trigger full rebuild; coordinate with TTL validation
- Custom RDF properties (e.g., `stats:`) must be documented in property declarations (`rdfs:label`, `rdfs:comment`)
