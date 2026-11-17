# Orange Juice Impedance Spectroscopy Dataset

Electrical impedance spectra of commercial orange juices, collected for three experiments:

1. **Binary mixture**: one brand is gradually mixed into another.
2. **Adulteration**: a juice is gradually diluted with water.
3. **Brand classification**: pure juice of each of the four brands, recorded in several sample groups.

> **Paper:** Z. Kara, O. Aybar, M. Yücel, B. B. Üstündağ, *"Electrical Impedance Spectroscopic Sensing and Spectral Analysis for Liquid Authenticity: An Orange Juice Case Study"*, **Sensors** (MDPI), 2026, in press.
> **License:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may use the data for any purpose, including commercial use, provided you cite the paper (see [Citation](#citation)).

The machine-learning code that uses this data is in a separate repository: [Orange-Juice-EIS-ML-Codes](https://github.com/Zeynep-Kara/Orange-Juice-EIS-ML-Codes).

## Files

| File | Experiment | Rows | Iterations | Label column(s) |
|---|---|---|---|---|
| `merged_mixtures_full_experiments_orange.csv` | Binary mixture | 172,257 | 857 | `brand_I`, `brand_II`, `brand_III`, `brand_IV` |
| `merged_adulteration_experiments.csv` | Adulteration | 55,275 | 275 | `adulteration` |
| `merged_classification.csv` | Class classification | 220,698 | 1,098 | `Label`, `Index` |

## Measurement format

Each **iteration** is one full frequency sweep of **201 points**. The points are spaced logarithmically from **1 kHz to 1 MHz**, with each frequency 1.035× the previous one. So each iteration takes 201 rows, and all rows in an iteration share the same `Iteration` value and the same labels.

### Common columns

| Column | Description |
|---|---|
| `Iteration` | Sweep index (unique within each file) |
| `Hz` | Measurement frequency |
| `Time` | Timestamp of the measurement. The format differs between files. |
| `Impedance`, `ImpedancePhase` | Impedance magnitude and phase |
| `Resistance`, `Reactance` | Real and imaginary parts of the impedance |
| `Admittance`, `AdmittancePhase` | Admittance magnitude and phase |
| `Conductance`, `Susceptance` | Real and imaginary parts of the admittance |
| `SeriesCapacitance`, `ParallelCapacitance` | Equivalent capacitance (series and parallel model) |
| `SeriesInductance`, `ParallelInductance` | Equivalent inductance (series and parallel model) |
| `Dissipation`, `Quality` | Dissipation factor (D) and quality factor (Q) |
| `Vrms`, `Vreal`, `Vimag` | Voltage: RMS, real and imaginary parts |
| `Irms`, `Ireal`, `Iimag` | Current: RMS, real and imaginary parts |

## 1. Binary mixture: `merged_mixtures_full_experiments_orange.csv`

Four commercial brands are anonymised as **Brand I–IV**. Each run starts with 100% of one brand (Container I), and a second brand (Container II) is added step by step until the mixture is 50/50.

The columns `brand_I` to `brand_IV` give the fraction of each brand in the sample. In every row they add up to 1.

| Iterations | Container I | Container II |
|---|---|---|
| 0–85 | Brand III | Brand I |
| 86–167 | Brand IV | Brand II |
| 168–252 | Brand I | Brand IV |
| 253–320 | Brand II | Brand I |
| 321–390 | Brand IV | Brand I |
| 391–457 | Brand I | Brand II |
| 458–525 | Brand III | Brand II |
| 526–592 | Brand I | Brand III |
| 593–659 | Brand II | Brand III |
| 660–725 | Brand IV | Brand III |
| 726–790 | Brand II | Brand IV |
| 791–856 | Brand III | Brand IV |

## 2. Adulteration: `merged_adulteration_experiments.csv`

Each brand is diluted step by step with water. The `adulteration` column is the fraction of water in the sample. It goes from 0 (pure juice) to 0.5 (1:1 juice and water).

| Iterations | Brand |
|---|---|
| 0–69 | Brand I |
| 70–137 | Brand II |
| 138–204 | Brand III |
| 205–274 | Brand IV |

## 3. Brand classification: `merged_classification.csv`

| Column | Description |
|---|---|
| `Label` | Brand: `brand_I`, `brand_II`, `brand_III` or `brand_IV`. These are the same brands as in the mixture and adulteration experiments. |
| `Index` | Sample group (recording session) within the brand. The models use it to split train and test data by sample group. |

| Label | Sample groups (`Index`) | Iterations |
|---|---|---|
| `brand_I` | 0–3 | 257 |
| `brand_II` | 0–3 | 204 |
| `brand_III` | 0–6 | 460 |
| `brand_IV` | 0–2 | 177 |

## Citation

If you use this dataset, please cite:

> Z. Kara, O. Aybar, M. Yücel, B. B. Üstündağ, "Electrical Impedance Spectroscopic Sensing and Spectral Analysis for Liquid Authenticity: An Orange Juice Case Study", *Sensors* (MDPI), 2026, in press.

```bibtex
@article{kara2026orange,
  title   = {Electrical Impedance Spectroscopic Sensing and Spectral Analysis for Liquid Authenticity: An Orange Juice Case Study},
  author  = {Kara, Zeynep and Aybar, O{\u{g}}uzhan and Y{\"u}cel, Meri{\c{c}} and {\"U}st{\"u}nda{\u{g}}, Burak Berk},
  journal = {Sensors},
  publisher = {MDPI},
  year    = {2026},
  note    = {In press}
}
```

The volume, article number and DOI will be added once the paper is published.
