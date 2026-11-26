# Worksheet: constraint-based modelling in practice

**Systems Biology hands-on workshop · King's College London**

Name: ______________________________ &nbsp;&nbsp; Partner: ______________________________

Work through the notebook `CBM_workshop.ipynb` and fill in this sheet as you go. For every part:

1. **Predict** first, on paper, before you run any code. A guess with a reason is enough.
2. **Run** the notebook and complete the **TODO** cells.
3. **Record** the numbers in the tables.
4. **Explain** in the answer boxes: a number plus one or two sentences.

Your report (end of the sheet) is built from these answers. Flux units are mmol/gDW/h; growth is per hour.

---

## Part A · The medium is a constraint (25 min)

**✏️ Predict.** Glucose has 6 carbons, acetate 2. Without oxygen, which of these do you expect *E. coli* to grow on,
and why?

> &nbsp;
>
> &nbsp;

**Task A1.** Complete the carbon-source cell (each source at an uptake of 10, with and without oxygen) and fill in
the table.

| Carbon source | C atoms | Aerobic growth | Anaerobic growth | Aerobic growth per C-mmol |
|---|---|---|---|---|
| D-glucose | 6 | | | |
| D-fructose | 6 | | | |
| pyruvate | 3 | | | |
| D-lactate | 3 | | | |
| succinate | 4 | | | |
| L-malate | 4 | | | |
| fumarate | 4 | | | |
| 2-oxoglutarate | 5 | | | |
| L-glutamate | 5 | | | |
| acetate | 2 | | | |
| ethanol | 2 | | | |

**Q A1.** Which carbon sources support growth without oxygen, and which do not? Suggest why (think about how ATP and
NAD⁺ are regenerated without respiration).

> &nbsp;
>
> &nbsp;
>
> &nbsp;

**Q A2.** Glucose gives the highest growth per mmol. Is it also the best *per carbon atom*? What does that tell you
about comparing growth rates on different substrates?

> &nbsp;
>
> &nbsp;

**Task A2 (genome scale).** Run the iJO1366 cell.

| Carbon source | iJO1366 aerobic | iJO1366 anaerobic | Core model aerobic (from A1) |
|---|---|---|---|
| D-glucose | | | |
| glycerol | | | — |
| succinate | | | |
| acetate | | | |
| D-xylose | | | — |

**Q A3.** iJO1366 can grow on xylose and glycerol; the core model has no reactions for them. Which model would you
use to predict growth on a new substrate, and why?

> &nbsp;
>
> &nbsp;

---

## Part B · Which nutrient limits growth? A phenotypic phase plane (25 min)

**✏️ Predict.** Sketch what you expect growth to look like as glucose uptake (x axis, 0–20) and oxygen uptake
(y axis, 0–30) increase. Where do you expect acetate to be secreted?

```
 O2 30 |
       |
       |
       |
       |
     0 +----------------------------
       0           glucose          20
```

**Task B1.** Complete the phase-plane cell (set the two lower bounds, optimise, store growth and acetate).

**Q B1.** At a glucose uptake of 10, above which oxygen uptake does growth stop increasing? What is the
O₂ : glucose ratio on the line of optimality, and how does it compare with the 6 : 1 of complete respiration?

| O₂ where growth stops increasing (glucose 10) | O₂ : glucose ratio on the line | compared with 6 : 1 |
|---|---|---|
| | | |

> &nbsp;
>
> &nbsp;

**Q B2.** Where in the plane is acetate secreted? Explain this "overflow metabolism" using Tuesday's
respire-or-ferment exercise.

> &nbsp;
>
> &nbsp;
>
> &nbsp;

**Q B3 (shadow prices).** Record the shadow prices at one point above and one below the line of optimality.

| Point | Growth | Shadow price glc__D_e | Shadow price o2_e |
|---|---|---|---|
| glucose 10, O₂ 30 | | | |
| glucose 10, O₂ 10 | | | |

Which nutrient has a non-zero shadow price in each region, and what does that mean?

> &nbsp;
>
> &nbsp;

---

## Part C · Growth or product? Objectives and trade-offs (25 min)

**✏️ Predict.** Without oxygen, can *E. coli* make more ethanol by growing less? Sketch the shape you expect for
"maximal ethanol" against growth rate.

> &nbsp;
>
> &nbsp;

**Task C1.** Run the production envelope, then complete the product cell.

Anaerobic maximal growth: ____________

| Product | Max (any growth) | Min at max growth | Max at max growth | Growth-coupled? (yes / no) |
|---|---|---|---|---|
| ethanol | | | | |
| acetate | | | | |
| formate | | | | |
| lactate | | | | |
| succinate | | | | |

**Q C1.** What is the maximal ethanol secretion without growth, and at maximal growth? Explain the trade-off in
terms of where the carbon and the ATP go.

> &nbsp;
>
> &nbsp;

**Q C2.** A product is *growth-coupled* if the cell must make it in order to grow at its maximum (minimum > 0 at
maximal growth). Which products are growth-coupled anaerobically? Why is growth coupling attractive for metabolic
engineering (think of OptKnock)?

> &nbsp;
>
> &nbsp;

**Q C3.** Last week you maximised ATP maintenance with oxygen (175 mmol from 10 glucose). Without oxygen:

Maximal ATP from 10 glucose: ____________ &nbsp; Main secreted products: ______________________________

Why is it more than 2 ATP per glucose?

> &nbsp;
>
> &nbsp;

---

## Part D · One optimum, many solutions (30 min)

**✏️ Predict.** FBA gives one flux for every reaction. Do you think that value is the only one compatible with
maximal growth? Guess how many of the 95 reactions could still vary.

Guess: ____________

**Task D1.** Run FBA and pFBA, and complete the FVA cell (at 100% and 90% of the optimum).

| | FBA | pFBA |
|---|---|---|
| Growth | | |
| Total absolute flux | | |

| | at 100% of max growth | at 90% of max growth |
|---|---|---|
| Number of reactions that can vary | | |

**Q D1.** How many reactions can vary at the optimum, and at 90% of it? What does this say about how precisely FBA
determines individual fluxes?

> &nbsp;
>
> &nbsp;

**Q D2.** FRD7 and SUCDi have huge ranges in ordinary FVA. Look up both reactions (`core.reactions.FRD7`). Why can
they carry any flux without changing anything else, and why does loopless FVA remove this?

| | ordinary FVA (min – max) | loopless FVA (min – max) |
|---|---|---|
| FRD7 | | |
| SUCDi | | |

> &nbsp;
>
> &nbsp;

**Task D2.** Run the sampling cell (about a minute) and fill in the table.

| Reaction | FBA | pFBA | FVA 90% min | FVA 90% max | Sample mean |
|---|---|---|---|---|---|
| PGI | | | | | |
| G6PDH2r | | | | | |
| PFK | | | | | |
| CS | | | | | |

**Q D3.** For PGI (glycolysis) and G6PDH2r (pentose phosphate pathway), compare the FBA value, the FVA range and the
sample distribution. Which one would you report if someone asked "how much flux goes through the pentose phosphate
pathway?", and why?

> &nbsp;
>
> &nbsp;
>
> &nbsp;

---

## Part E · What happens when genes are deleted? (25 min)

**✏️ Predict.** *pgi* (phosphoglucose isomerase) is not essential on its own. Which other genes do you expect to
become essential when *pgi* is deleted? Write two or three, with a reason.

> &nbsp;
>
> &nbsp;

**Task E1.** Complete the double-deletion cell.

Essential genes: ________ &nbsp; Non-essential genes: ________ &nbsp; Synthetic lethal partners of *pgi*: ________

**Q E1.** List the synthetic lethal partners of *pgi* and group them by reason.

| Group (reason) | Genes |
|---|---|
| alternative route for glucose-6-phosphate | |
| other / not obviously related | |

Challenge: without PGI, all glucose goes through the oxidative pentose phosphate pathway, which makes NADPH. Why
might complex I (*nuo* genes) then become essential? Compare NADTRHD and NADH16 in the wild type and the *pgi*
mutant (e.g. with `pfba()`).

| | wild type | *pgi* mutant |
|---|---|---|
| NADTRHD (transhydrogenase) | | |
| NADH16 (complex I) | | |

> &nbsp;
>
> &nbsp;
>
> &nbsp;

**Task E2.** Complete the FBA-versus-MOMA cell.

| Knockout | FBA growth | MOMA growth (linear) |
|---|---|---|
| pgi (b4025) | | |
| zwf (b1852) | | |
| tpiA (b3919) | | |
| gltA (b0720) | | |
| sdhA (b0723) | | |

**Q E2.** For which knockouts do FBA and MOMA disagree most? Which prediction would you expect to match a freshly
made mutant, and which one the same mutant after weeks of adaptive laboratory evolution? (And why must MOMA's
reference be the *wild-type* solution?)

> &nbsp;
>
> &nbsp;
>
> &nbsp;

**Q E3 (optional, ~2 min).** Run `double_gene_deletion(core, gene_list1=non_essential)` for all pairs. How many
synthetic lethal pairs are there? Pick one pair not discussed in the lecture and explain it from the reactions.

Number of synthetic lethal pairs: ____________

> &nbsp;
>
> &nbsp;

---

## Part F · What happens over time? Dynamic FBA (25 min)

**✏️ Predict.** In a batch culture that starts with 20 mM glucose and limited oxygen, what happens to acetate over
time? Sketch biomass, glucose and acetate against time.

```
conc. |
      |
      |
      |
    0 +----------------------------
      0            time (h)          14
```

**Task F1.** Run the dynamic FBA cell, then complete the cell that repeats it at four oxygen supplies.

| O₂ max | Max acetate (mM) | Glucose gone at (h) | Final biomass (gDW/L) |
|---|---|---|---|
| 2 | | | |
| 8 | | | |
| 15 | | | |
| 25 | | | |

**Q F1.** Describe the two growth phases in the oxygen-limited batch (O₂ ≤ 8). What is a diauxic shift, and why does
the model use glucose before acetate?

> &nbsp;
>
> &nbsp;

**Q F2.** How do maximal acetate and final biomass change with the oxygen supply? Relate this to your phase plane
from Part B.

> &nbsp;
>
> &nbsp;

**Q F3.** Name two things this dynamic FBA leaves out that a real batch culture has (hint: regulation, lag phases,
oxygen transfer).

> &nbsp;
>
> &nbsp;

---

## Report

Write a short report of **about 4 pages** (figures and tables included; references and code appendix not counted),
built from your answers on this sheet and the notebook outputs.

**Include:** T1 carbon-source table (A1) · F1 phase plane with the line of optimality (B1) · F2 production envelope
(C) · T2 growth-coupling table (C1) · F3 FVA ranges or sampling distributions (D) · T3 FBA vs MOMA table (E2) ·
F4 dynamic FBA time courses (F1). Every figure needs a caption with the model, medium and constraints.

**Answer, one section each:**

1. **Constraints.** Using Parts A and B, explain how the medium (carbon source, oxygen) constrains the predicted
   phenotype. Which nutrient limits growth in each region, and how do the shadow prices show it?
2. **Objective functions.** Using Part C, compare growth, ATP production and product secretion as objectives. When
   is maximal growth a reasonable assumption, and when is it not? Why is growth coupling useful?
3. **Uncertainty.** Using Part D, discuss how precisely FBA determines individual fluxes. When would you report an
   FBA/pFBA value, an FVA range or a sampled distribution? What are loops, and why remove them?
4. **Genetic perturbations.** Using Part E, explain two synthetic lethal pairs from the network, and the difference
   between FBA and MOMA. Which would you trust for a fresh knockout, and which after adaptive evolution?
5. **Dynamics.** Using Part F, explain what dynamic FBA adds to FBA, and its main limitations.
6. **Reflection (short).** One limitation of constraint-based modelling this workshop made clear, and one kind of
   data that could reduce it.

**Structure:** introduction (~½ page) · results and discussion, one section per question · conclusion (3–5
sentences) · references · appendix with the code you wrote.

**Marking:** correct results 30% · biological interpretation 35% · critical view of the method 20% · clarity
(captions, structure, length) 15%. A good answer gives the number **and** explains it from the network.

## Notes

> &nbsp;
>
> &nbsp;
>
> &nbsp;
