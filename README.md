# EEG motor imagery classification

This project investigates how EEG frequency band selection affects within subject classification of imagined hand versus foot movements. The same analysis is repeated independently across ten subjects to examine how consistent the effect is between individuals.

## Dataset and method

The analysis uses subjects 1–10 from the [EEGBCI motor imagery dataset](https://physionet.org/content/eegmmidb/1.0.0/). For each subject, runs 6, 10, and 14 are loaded. The analysis keeps 15 motor-cortex channels: `FC3, FC1, FCz, FC2, FC4, C3, C1, Cz, C2, C4, CP3, CP1, CPz, CP2, CP4`.

For each of three bands (8–13 Hz, 13–30 Hz, and 8–30 Hz), the signal is band-pass filtered, epoched from 1 to 2 seconds after each cue, and converted to log-variance power features, one feature per channel. A standardized logistic regression classifier is evaluated with leave-one-recording-run-out validation. The parameters and processing order are defined in `analysis.ipynb`.

## Results

The saved subject-level results are in [`results/results.csv`](results/results.csv), and the final figure is [`figures/frequency_band_accuracy.png`](figures/frequency_band_accuracy.png).

| Frequency band | Mean accuracy | Standard deviation |
|---|---:|---:|
| 8–13 Hz | 0.660000 | 0.102131 |
| 13–30 Hz | 0.631111 | 0.148961 |
| 8–30 Hz | 0.631111 | 0.094397 |

Across the ten subjects, 8–13 Hz achieved the highest mean accuracy at 66.0%, compared with 63.1% for both 13–30 Hz and 8–30 Hz. However, performance varied substantially between subjects, indicating that the most informative frequency range may be subject dependent.are descriptive for the ten analyzed subjects and three selected recording runs. They do not establish generalization to other subjects, sessions, preprocessing choices, or classifiers.

## Reproduce

1. Create an environment and install the dependencies from `requirements.txt`.
2. Open and run all cells in `analysis.ipynb`.
3. MNE will download the EEGBCI EDF files from PhysioNet on first use and cache them locally.

The notebook writes `results/results.csv` and regenerates `figures/frequency_band_accuracy.png`.
