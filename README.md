# Less light for the same signal: scan gating and pulse picking for two-photon imaging of the retina

Analysis code for the article of the same title by P. Gläser, Q. Yang, C. Bergmann, X. Xie, Z. Zhao and C. Schwarz (submitted).

Data: https://doi.org/10.5281/zenodo.24494777

## Notebooks

`oscilloscope_analysis.ipynb`
Photodiode recordings of the pulse train after the Pockels cell with pulse picking to 40 and 20 MHz (Fig. 4). Duty cycle, interval and height of the pulses, leaked pulses and the two-photon gain expected from the pulse train.

`pulse_picking_analysis.ipynb`
Ex vivo mouse retina, five illumination configurations at 2 mW. Dark and offset correction, two-photon and confocal signal, gains, bleaching and repeats. Makes Figs. 5 and 6 and Supplementary Figs. 1 to 11, writes the values per recording behind Supplementary Table 1 to `data/derived/summary.csv` and the numbers quoted in the article to `data/derived/manuscript_numbers.json`.

| Article | Notebooks | Configuration |
|---|---|---|
| C0 | case0 | conventional illumination, 80 MHz |
| C1 | case1 | edge blanking, 80 MHz |
| C2 | case2 | backward scan blanking, 80 MHz |
| C3 | case3 | backward scan blanking, 40 MHz |
| C4 | case4 | backward scan blanking, 20 MHz |

## Setup

```
conda env create -f environment.yml
conda activate pulse-picking
jupyter lab
```

or `pip install -r requirements.txt` with Python 3.11.

Download `derived.zip` and `oscilloscope.zip` from the Zenodo record above and unpack both into `data/`:

```
data/
  derived/
    2026-09-10/
    2026-09-29/
    2026-10-09/
    2026-10-15/
  oscilloscope/
    2026-10-12_20mhz.CSV
    2026-10-12_40mhz.CSV
```

## Running

Run `oscilloscope_analysis.ipynb` first. It caches the photodiode traces in `data/derived/oscilloscope/`, which the last cell of `pulse_picking_analysis.ipynb` reads. Figures are saved to `figures/`.

The first section of `pulse_picking_analysis.ipynb` (Videos -> tif) averages the raw videos into `data/derived/`. It is skipped for every session that already has a `recordings.csv`, so the raw videos are not needed to reproduce the results. To rebuild a session from the videos, put them in `data/raw/<session>/` and delete `data/derived/<session>/recordings.csv`.

## License

Code: MIT, see `LICENSE`. Data: CC BY 4.0.
