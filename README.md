# Avalanche activity forecasting with LSTM

Small deep-learning coursework project: daily **Avalanche Activity Index (AAI)** style targets around **Davos (Switzerland)** are modeled with stacked **LSTMs** in **PyTorch**, using public hazard, observation, and weather tables. The notebook also explores **outlier cleaning**, **thresholded metrics**, a **persistence baseline**, **tail-risk hits**, and a **Utah (Alta–Collins)** generalization experiment with optional **fine-tuning**.

**Author:** Fernando Sampalo

## Repository layout

| Item | Description |
|------|-------------|
| `lstm.ipynb` | Main notebook (English comments and narrative). Run top to bottom after installing dependencies. |
| `report.pdf` | Written report (if present in your copy). |
| `requirements.txt` | Python dependencies. |
| `LICENSE` | MIT license for code and docs in this repo. |
| `CITATION.cff` | Machine-readable citation metadata for GitHub. |
| `.gitignore`, `.gitattributes`, `.editorconfig`, `.env.example` | Tooling and local config template. |
| `data_set_*.csv`, `davos_weather_*.csv`, `CLN_*.csv` | Input CSVs (semicolon-separated where applicable). |
| `photos/` | Exported figures from the experiments. |

A Google Drive mirror for the datasets is linked at the top of the notebook for convenience.

## Setup

Python 3.10+ recommended.

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

Then open `trabajo_fernandosampalo.ipynb` in Jupyter, VS Code, or Cursor and **run all cells**. Figures are saved next to the notebook and under `photos/` when paths in the code point there (adjust `plt.savefig` paths if you reorganize folders).

## Methods (high level)

- **Sequence model:** two-layer LSTM (`AvalancheLSTM` / `AvalancheLSTMFull`) with dropout and dense head; **weighted MSE** to emphasize larger targets; early stopping on validation loss.
- **Data:** incomplete four-column pipeline vs merged eight-feature pipeline; optional **winter–spring** seasonal mask.
- **Outliers:** IQR-based flags with linear interpolation before scaling.
- **Evaluation:** RMSE/MAE, persistence baseline, critical-day hit rate, Utah transfer with scaler `transform` only and light head fine-tuning.

## Note on outputs

Notebook **code outputs were cleared** so the file stays smaller and only English source is versioned. Re-run the notebook to regenerate prints and plots.

## Citation

GitHub can generate a citation snippet from [`CITATION.cff`](CITATION.cff). Replace the placeholder `repository-code` URL with your public clone, or cite manually:

> Fernando Sampalo. *Avalanche activity forecasting with LSTM* (2026). Source code and documentation.

## License

- **Code and documentation** in this repository (notebook, LaTeX, scripts, `README`, etc.) are released under the [MIT License](LICENSE) unless a file states otherwise.
- **Bundled CSV datasets** may be subject to upstream publisher terms. See [`NOTICE`](NOTICE) before redistributing raw data outside your fork.