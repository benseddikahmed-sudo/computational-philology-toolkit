# computational-philology-toolkit
# Computational Detection of Numerical Patterns in Ancient Texts

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Supplementary code for the manuscript submitted to *Digital Scholarship in the Humanities* (DSH).

## 📋 Overview

This repository provides a reproducible computational pipeline for analyzing numerical patterns in ancient texts, with particular focus on:

- **Gematria analysis** (Hebrew alphanumeric values)
- **Statistical testing** of numerical hypotheses (divisibility patterns, age distributions)
- **Equidistant Letter Sequences (ELS)** with Monte Carlo testing
- **Cross-corpus comparison** (Hebrew, Greek, Latin texts)
- **Bayesian inference** for proportion estimation
- **Multiple testing correction** (FDR, Bonferroni)

## 🚀 Quick Start

### Installation

```bash
# Clone or download the repository
git clone https://github.com/yourusername/computational-numerical-patterns.git
cd computational-numerical-patterns

# Install dependencies
pip install -r requirements.txt
```

### Basic Usage

```bash
# Run the full pipeline with default settings
python computational_detection_of_numerical_patterns.py

# View help and options
python computational_detection_of_numerical_patterns.py --help

# Run with custom parameters
python computational_detection_of_numerical_patterns.py \
    --data-dir ./my_data \
    --n-els 5000 \
    --correction-method fdr_bh \
    --seed 42
```

### Expected Output

```
data/results/YYYYMMDD_HHMMSS/
├── results_summary.json      # Complete numerical results
├── ages_hist.png             # Age distribution comparison
└── posterior_bands.png       # Bayesian posterior intervals
```

## 📁 Project Structure

```
.
├── computational_detection_of_numerical_patterns.py  # Main pipeline
├── test_computational_detection.py                   # Unit tests
├── requirements.txt                                  # Python dependencies
├── README.md                                         # This file
├── data/                                             # Data directory
│   ├── genesis_numerical.csv                        # Numerical data from Genesis
│   ├── control_numerical.csv                        # Control dataset
│   ├── full_genesis_hebrew.txt                      # Hebrew text (optional)
│   ├── homer_iliad_greek.txt                        # Greek comparison text
│   ├── virgil_aeneid_latin.txt                      # Latin comparison text
│   └── results/                                      # Output directory (auto-generated)
└── docs/                                             # Additional documentation
    └── METHODOLOGY.md                                # Detailed methods
```

## 📊 Data Format

### Input Files

#### 1. `genesis_numerical.csv`

Required columns:
- `name`: String identifier (person name or Hebrew term)
- `value`: Integer numerical value (age or gematria)
- `type`: Category type (`age`, `gematria`, etc.)
- `category`: Subcategory (`antediluvian`, `postdiluvian`, `hebrew_term`, etc.)
- `source`: Biblical reference or calculation method

Example:
```csv
name,value,type,category,source
Adam,930,age,antediluvian,Genesis 5:5
Seth,912,age,antediluvian,Genesis 5:8
בראשית,913,gematria,hebrew_term,calculated
```

#### 2. Text Files (Optional)

Plain text files containing Hebrew, Greek, or Latin characters. If absent, the pipeline generates placeholder texts for testing purposes.

**Note**: Due to copyright restrictions, original texts are not included in this repository. Users should obtain texts from authorized sources (e.g., Sefaria.org for Hebrew texts, Perseus Digital Library for Greek/Latin).

## 🔬 Methodology

### Statistical Tests

1. **Binomial Tests**: Test for non-random divisibility patterns
2. **Mann-Whitney U Test**: Compare antediluvian vs postdiluvian ages
3. **Monte Carlo Permutation**: ELS significance testing
4. **Bayesian Inference**: Beta-Binomial posterior estimation

### Multiple Testing Correction

The pipeline automatically applies correction for multiple comparisons using:
- **Benjamini-Hochberg FDR** (default, recommended)
- **Bonferroni correction** (conservative)
- **Holm-Bonferroni** (step-down procedure)

### ELS Analysis: Important Limitations

⚠️ **Critical Methodological Note**: The ELS analysis uses a simplified character-permutation null model that preserves only unigram frequencies. This approach has significant limitations:

- Does **NOT** account for higher-order linguistic structure (bigrams, morphology)
- May detect patterns arising from natural language structure rather than intentional encoding
- Subject to multiple testing and researcher degrees of freedom

**Recommended reading**:
- McKay, B. D., Bar-Natan, D., Bar-Hillel, M., & Kalai, G. (1999). Solving the Bible code puzzle. *Statistical Science*, 14(2), 150-173.
- Bar-Hillel, M., Bar-Natan, D., & McKay, B. D. (1998). The Torah codes: puzzle and solution. *Chance*, 11(2), 13-19.

For rigorous research, consider:
- Markov chain null models preserving n-gram structure
- Control texts matched for linguistic properties
- Pre-registration of hypotheses and target sequences

## 🧪 Testing

Run the test suite to verify correct installation:

```bash
# Run all tests
pytest test_computational_detection.py -v

# Run specific test
pytest test_computational_detection.py::test_gematria_basic -v

# Generate coverage report
pytest --cov=computational_detection_of_numerical_patterns \
       --cov-report=html \
       test_computational_detection.py
```

## 📈 Reproducibility

### Deterministic Results

The pipeline uses fixed random seeds by default (seed=42). To verify reproducibility:

```bash
# Run 1
python computational_detection_of_numerical_patterns.py --seed 42

# Run 2 (should produce identical results)
python computational_detection_of_numerical_patterns.py --seed 42
```

### System Information

Each run automatically records:
- Python and package versions
- MD5 checksums of input data
- Dataset sizes and preprocessing steps
- Complete configuration parameters

This information is saved in `results_summary.json` for full traceability.

## 🎓 Citation

If you use this code in your research, please cite:

```bibtex
@article{YourName2025computational,
  title={Computational Detection of Numerical Patterns in Ancient Texts},
  author={Your Name and Co-Authors},
  journal={Digital Scholarship in the Humanities},
  year={2025},
  volume={XX},
  number={X},
  pages={XXX--XXX},
  doi={10.1093/llc/fqXXXXXX}
}
```

## 🤝 Contributing

This code is provided as supplementary material for peer review. For questions or suggestions:

1. Open an issue on GitHub
2. Contact: Ahmed Benseddik <contact@example.org>

## ⚖️ Ethical Considerations

This analysis treats religious texts as historical-linguistic artifacts for academic study. It does **not** make theological claims about divine authorship or prophetic encoding. 

Researchers should:
- Respect the religious significance of these texts to practitioners
- Clearly distinguish between statistical patterns and theological interpretations
- Avoid sensationalist claims not supported by rigorous evidence
- Acknowledge limitations and alternative explanations

## 📜 License

MIT License - see LICENSE file for details.

Copyright (c) 2025 Ahmed Benseddik and Research Team

## 🔗 Resources

### Data Sources
- [Sefaria.org](https://www.sefaria.org/) - Hebrew Biblical texts
- [Perseus Digital Library](http://www.perseus.tufts.edu/) - Greek and Latin classics
- [Mechon Mamre](https://www.mechon-mamre.org/) - Masoretic text

### References
- Anthropic Documentation: [https://docs.anthropic.com](https://docs.anthropic.com)
- DSH Journal: [https://academic.oup.com/dsh](https://academic.oup.com/dsh)
- Statistical Methods: Wasserman, L. (2004). *All of Statistics*. Springer.

## 📞 Support

For technical issues:
- Check the [FAQ](docs/FAQ.md)
- Review [METHODOLOGY.md](docs/METHODOLOGY.md)
- Open a GitHub issue

For methodological questions:
- Consult the manuscript and supplementary materials
- Contact the corresponding author

---

**Version**: 1.1  
**Last Updated**: September 29, 2025  
**Status**: Submitted to DSH for peer review
