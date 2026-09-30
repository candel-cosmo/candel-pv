# candel-pv

Peculiar-velocity forward models for CANDEL. A probe package for
[CANDEL](https://github.com/candel-cosmo/CANDEL), part of the
[candel-cosmo](https://github.com/candel-cosmo) organisation. It imports the
core `candel` library; the core never imports it. See the
[CANDEL README](https://github.com/candel-cosmo/CANDEL#how-the-repositories-fit-together)
for how the repositories fit together.

## What it provides

Forward models for peculiar-velocity catalogues, jointly calibrating each
distance-indicator relation and a reconstructed density/velocity field
(amplitude $\beta$, external bulk flow $\mathbf{V}_\mathrm{ext}$, galaxy bias,
density-dependent velocity dispersion).

- **Tully--Fisher:** 2MTF, SFI++, CF4-TFR (`model_PV_TFR.py`)
- **Type Ia supernovae (SALT2):** LOSS, Foundation, Pantheon+ (`model_PV_SN.py`, `model_PV_PantheonPlus.py`)
- **Fundamental Plane:** 6dFGS-FP, SDSS-FP (`model_PV_FP.py`)
- Growth rate / $S_8$ (`growth_rate.py`), mocks (`mock.py`) and the
  redshift-to-real-space mapping (`redshift2real/`)

Multiple catalogues can be fitted jointly with shared parameters. Runs set
`model.which_run = "PV"`, or leave it unset.

## Install

Clone this repository next to the CANDEL core and install both, core first:

```bash
git clone https://github.com/candel-cosmo/CANDEL.git
git clone https://github.com/candel-cosmo/candel-pv.git
cd CANDEL
python -m venv venv_candel && source venv_candel/bin/activate
pip install -e .
pip install --no-deps -e ../candel-pv
```

Data, results and the machine-local `local_config.toml` live in the CANDEL
checkout. Python code finds it through the installed `candel`
(`candel.util.CANDEL_ROOT`); shell scripts use `$CANDEL_ROOT`, defaulting to
`../CANDEL`.

## Layout

- `candel_pv/` — the package
- `configs/` — run configurations
- `scripts/` — preprocessing, mocks and submission helpers
- `papers/` — scripts and notebooks behind each paper
- `tests/` — tests (`pytest`)

## Papers

- `papers/H0_dipole/` — No evidence for $H_0$ anisotropy, [arXiv:2509.14997](https://arxiv.org/abs/2509.14997)
- `papers/S8/` — $S_8$ from TFR, FP and SN distances, [arXiv:2509.20235](https://arxiv.org/abs/2509.20235)
- `papers/VFO/` — The Velocity Field Olympics, [arXiv:2502.00121](https://arxiv.org/abs/2502.00121)

## Run

```bash
python ../CANDEL/scripts/runs/main.py --config configs/config.toml
```

Batch grids are defined in `candel_pv/specs.py` and built with the core's
`scripts/runs/generate_tasks.py`.

## License

MIT; see `LICENSE`.
