# Stochastic Simulation of Fitness Effects Across Genetic Backgrounds

This MATLAB project simulates how genetic variation influences the fitness impact of a mutation by modeling stochastic gene expression and enzymatic activity in a metabolic pathway. The model captures single-cell dynamics across multiple strains and regulatory settings.

---

## 📂 Files

- **`run_simulation.m`** — Main script that performs the simulation for 20 strains and 26 genetic backgrounds per strain. Simulates cell growth pre- and post-mutation.
- **`enzyme_gen.m`** — Function that models stochastic gene expression over time, producing mRNA and protein bursts.
- **`stoch.m`** — (Expected) Helper function that determines the number of stochastic bursts based on a distribution.
- **`stopEvent.m`** — Event function used by the ODE solver to stop integration when all three key metabolites (S3, S5, S7) reach depletion thresholds.
- **`testfile.xlsx`** — Output file containing single-cell division times before and after mutation for each genetic background and strain.

---
# This code reports the fitness values obtained for two values of ton1 (0.5 and 1) in 25 cells of 20 differnt strains, when the background variation is in ton2 (See Methods for more details).  



This simulation models:
- **Enzyme Expression**: Using stochastic burst models of mRNA/protein synthesis.
- **Metabolism**: Three metabolites are consumed during cell growth via enzymatic reactions.
- **Fitness**: Time to division (when all key metabolites are depleted) is used as a proxy for fitness.
- **Mutation**: A change in `ton1` mimics a mutation. Its fitness effect is computed across diverse genetic backgrounds.

---

## ⚙️ How It Works

1. **Setup**: Each strain (20 total) contains 25 genetic backgrounds with randomized parameters (`toff`, `ton`, `kcat`, `Km`).
2. **Simulation**: For each background, simulate:
   - Stochastic enzyme production (`enzyme_gen`).
   - ODE-based resource consumption using `ode45`.
   - Cell division occurs when all key metabolites reach a depletion threshold.
3. **Mutation**: Repeat the simulation after altering `ton1` (from 0.5 to 1).
4. **Output**: Store the division time (`tdiv`) and metabolite levels in `testfile.xlsx`.

---

## 📈 Output Format

`testfile.xlsx` contains:
- `tot_tdiv`: Time to cell division (fitness proxy).

---

## ▶️ Running the Code

1. Open MATLAB.
2. Ensure all `.m` files are in the same directory.
3. Run the main script: mainfile.m
4. The output will be returned with the fitness values in an excel file with (101 x 25 x 20 entries). 

# in the excel file
1. Every odd numbered row corresponds to the division times of a cell when ton1=0.5, and even numbered row the fitness when ton1=1. For example, the entries in row 1 correspond to the division times in a given background when ton1=0.5,
and row 2 entries are the division times in the same background when ton1=1.
2. For a particular row, to measure the average fitness of a cell, measure the differences in the division time by subtracting the entry in column n-1 from the entry in column n, and averaging these differences. 
3. In a background, the fitness effect of the ton1 mutation = fitness in an even numbered row - fitness in the just preceding odd numebred row
4. After every 2 rows, the background changes within a strain. 
5. After every 50 rows, the strain changes, i.e., rows 1:50 = strain 1, rows 51:100 = strain 2, and so on.  