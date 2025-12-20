# HVDNet Vocabularies

This repository hosts a collection of controlled vocabularies developed and maintained by the [**High-Value Data Network**](https://highvaluedata.net). The vocabularies are designed to provide standard, structured sets of concepts and terms for describing and organizing data across various domains and use cases.

## Vocabularies

### Statistics Vocabulary

The descriptive statistics vocabulary provides a controlled set of concepts for describing statistical measures and summary statistics for FAIR data. It is modeled using [SKOS](https://www.w3.org/2004/02/skos/) (Simple Knowledge Organization System).

**Status**: Early development — not intended for production use.

**Source**: [statistics.ttl](./statistics.ttl)

#### Structure

The statistics vocabulary is organized into several categories:
- **Central Tendency/Location**: Arithmetic mean, Geometric mean, Median, Mode, Quartiles, Percentiles, etc.
- **Dispersion/Variability**: Variance, Standard Deviation, Range, IQR, MAD, Gini coefficient, etc.
- **Association/Dependence**: Covariance, Pearson/Spearman/Kendall correlations, etc.
- **Shape/Distribution**: Skewness, Kurtosis, Normality tests (Shapiro-Wilk, Anderson-Darling, etc.)
- **Robust Statistics**: Trimmed mean, Winsorized mean, Trimean, Biweight midvariance, Qn/Sn estimators
- **Size/Count**: Valid/Invalid cases, Sample size, Unique cases, Frequency, Sparsity, etc.
- **Derived Ratios**: Coefficient of variation, Z-scores, Shares, Rates, etc.
- **Missingness/Completeness**: Missing rate, Non-null rate
- **Outliers**: Outlier counts (IQR-based, Z-score-based)
- **Information Content**: Shannon entropy
- **Text Measures**: Length statistics, Word counts, Lexical diversity, Languages
- **File-level Statistics**: Record/Variable counts, File size, Checksum, Encoding, MIME type, etc.
- **Categorical Profiling**: Top-k categories, Category shares, Cardinality buckets, Imbalance ratio

Each concept includes:
- **skos:scopeNote**: Human-readable computation guidance
- **stats:formula**: Mathematical formula (LaTeX notation) where applicable
- **stats:computationMethod**: Step-by-step textual computation instructions

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

