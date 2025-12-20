# HVDNet Vocabularies

This repository hosts a collection of controlled vocabularies developed and maintained by the [**High-Value Data Network**](https://highvaluedata.net). The vocabularies are designed to provide standard, structured sets of concepts and terms for describing and organizing data across various domains and use cases.

## Vocabularies

### Statistics Vocabulary

The descriptive statistics vocabulary provides a controlled set of concepts for describing statistical measures and summary statistics for FAIR data. It is modeled using [SKOS](https://www.w3.org/2004/02/skos/) (Simple Knowledge Organization System).

**Status**: Early development — not intended for production use.

**Source**: [statistics.ttl](./statistics.ttl)

#### Structure

The statistics vocabulary is organized into several categories:
- **Central Tendency/Location**: Mean, Median, Mode, etc.
- **Dispersion/Variability**: Variance, Standard Deviation, Range, etc.
- **Size/Count**: Valid/Invalid cases, Sample size, etc.
- **Other/Derived Ratios**: Z-score, Coefficient of variation, etc.
- **Shape/Distribution**: Skewness, Kurtosis, etc.
- **Text/String Measures**: Length, Word count, Lexical diversity, etc.
- **Metadata**: Technical metadata like ASCII indicators.

#### Related Resources

This vocabulary complements existing standards, including the [DDI Alliance controlled vocabulary for summary statistics](https://rdf-vocabulary.ddialliance.org/ddi-cv/SummaryStatisticType/2.1.2/SummaryStatisticType.html). Many concepts are also available on [Wikidata](https://www.wikidata.org/), enabling interoperability with linked data resources and knowledge graphs.

### Future Vocabularies

Additional vocabularies will be added to this collection over time.

## Publishing

Vocabularies are published using [SkoHub Pages](https://github.com/skohub-io/skohub-pages).

## Feedback

We welcome feedback, suggestions, and comments. Please use [GitHub issues](https://github.com/hvdnet/hvdnet-vocabs/issues) to contribute.

## License

These vocabularies are licensed under the [CC0 1.0 Universal (CC0 1.0) Public Domain Dedication](https://creativecommons.org/publicdomain/zero/1.0/).

