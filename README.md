# Constraint-based modelling in practice

A hands-on workshop (about 3 hours) for the Systems Biology module (7BBG1004) and the MSc Microbiome in Health and
Disease, King's College London. This morning's lecture introduced the constraint-based toolbox. In this workshop
you use each tool yourself on real models of *E. coli*: different media, phase planes, production envelopes, pFBA,
FVA, flux sampling, synthetic lethality, MOMA and dynamic FBA.

It follows on from last week's workshop on GEMs and the stoichiometric matrix.

## What you need

- `CBM_workshop.ipynb`: the notebook you work in
- `worksheet/worksheet.md` (or the printable `worksheet/worksheet.html`): the tasks and questions, with space for
  your answers. Fill it in as you go: the report questions at the end are built from it.
- `slides/`: the short deck shown at the start of each part
- Python 3.9 to 3.12 with cobrapy, plotly and Jupyter
- Internet access: the two models are downloaded by cobrapy the first time you load them

## Set up (once, before the session)

**With Anaconda or Miniconda** (recommended):

```bash
conda create -n cbm python=3.11
conda activate cbm
pip install -r requirements.txt
```

**With plain Python:** open a terminal (Mac) or Command Prompt (Windows) and run

```bash
python -m pip install -r requirements.txt
```

(On Windows, if `python` opens the Microsoft Store, use `py -m pip install -r requirements.txt` instead.)

Then download this repository (green **Code** button → *Download ZIP*, or `git clone`), start Jupyter in its folder
and open the notebook:

```bash
jupyter notebook
```

Run the first code cell. If it prints `cobra 0.32` (or newer) and `95 reactions`, you are ready.

## Contents

| Part | Question | Method | Time |
|---|---|---|---|
| A | What can *E. coli* grow on? | FBA with different media | 25 min |
| B | Which nutrient limits growth? | phenotypic phase plane, shadow prices | 25 min |
| C | Growth or product? | production envelope, other objectives | 25 min |
| – | break | | 15 min |
| D | One optimum, many solutions | pFBA, FVA, loopless FVA, sampling | 30 min |
| E | What happens when genes are deleted? | synthetic lethality, FBA vs MOMA | 25 min |
| F | What happens over time? | dynamic FBA | 25 min |

## How to work

- Run each cell with *Shift + Enter*, from the top.
- Cells marked **TODO** are yours to complete: replace each `...` with your code. Until you do, that cell (and
  sometimes a later cell that uses its result) will show an error. This is expected.
- Questions marked **Q** are on the worksheet. Write short answers: a number and one or two sentences of explanation.
- Before each part, write down your **prediction** on the worksheet first, then run the code. Being wrong is the
  useful part.
- If the notebook gets into a strange state: *Kernel → Restart & Run All*.

Common pitfalls: uptake is a **negative** flux (`lower_bound = -10` allows uptake of 10); use `with model:` blocks
so your changes are undone; *infeasible* means a constraint cannot be met; cobrapy's shadow prices are negative for
metabolites that would increase growth.

Solutions are released after the session.

## Credits

Cheng Zhang, King's College London. Builds on the KCL Systems Biology notebooks (F. Clasen,
github.com/FrederickClasen/SysBio_tutorial) and last week's GEM and S-matrix workshop. Uses cobrapy (Ebrahim et al.,
*BMC Syst Biol* 2013), the *E. coli* core model (Orth et al., *EcoSal Plus* 2010) and iJO1366 (Orth et al.,
*Mol Syst Biol* 2011).

The material may be freely reused for teaching, with attribution.
