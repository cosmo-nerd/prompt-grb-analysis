# prompt-grb-analysis
#  Bangs, Blips and Background: Decoding GRB Signals

This project implements a pipeline to detect and classify Gamma-Ray Bursts (GRBs) from AstroSat-CZTI data using statistical methods and signal processing techniques. It distinguishes astrophysical transients from background noise and charged particle hits, establishing a framework for reliable GRB detection and analysis.

---

##  Project Structure

- `1_GRB_detection.ipynb`  
  Constructs light curves from AstroSat CZTI data and applies multiple detrending filters (Savitzky-Golay, Median, Wavelet) to highlight potential transient features.

- `2_pipeline.ipynb`  
  Performs peak detection using SNR analysis and n-sigma thresholding, followed by spectrogram generation and classification of events into:
  - **Bang (GRB)**
  - **Blip (charged particle)**
  - **Background (noise)**

- `Report.pdf`  
  A detailed report explaining the physics motivation, methodology, detector details, results, and conclusions of the study.

---

##  Methods Overview

###  Data Processing
- Raw CZTI quadrant and veto data parsed from `.evt` FITS files using `astropy`.
- Binned into 1s and 10s light curves across multiple energy bands (20–100 keV for CZT and 100-500keV for Veto).

###  Detrending
Applied and compared:
- **Savitzky-Golay filtering** (unsuitable due to peak smoothing)
- **Median filtering** (best performance for impulsive events)
- **Wavelet denoising** (balanced suppression but slightly smoothed peaks)
- **Matched filtering** (template mismatch issues for GRBs)

###  Peak Detection
- Used SNR calculation and **5σ thresholding** to identify statistically significant events.
- Spectrograms and energy-profile plots validate astrophysical signatures.

###  Classification Logic
1. **Bang (GRB)**: Multi-quadrant, multi-band, >5σ, power-law energy profile.
2. **Blip (Particle)**: Localized spike in one band/quadrant, 3σ–5σ range.
3. **Background**: Instrumental artifacts, noise, or post-SAA glitches.

---

##  Instrument: AstroSat-CZTI

The Cadmium Zinc Telluride Imager (CZTI) onboard AstroSat (India’s first space observatory) operates in the 20–200 keV range with a wide field-of-view. Its veto detectors (100–500 keV) help eliminate cosmic ray contamination. The data are quadrant-resolved and sensitive to GRBs both on- and off-axis.

---

##  Key Results

- Successfully recovered faint GRB candidates not captured by onboard triggers.
- Validated peaks through spectrograms and energy evolution patterns.
- Built a foundation for a future machine learning classifier on transient detection.

---

##  Requirements

- Python 3.8+
- numpy
- pandas
- matplotlib
- scipy
- astropy
- pywt (for wavelets)
- scikit-learn (for DBSCAN clustering)
- seaborn
- JupyterLab or Notebook

Install all dependencies:
```bash
pip install -r requirements.txt

