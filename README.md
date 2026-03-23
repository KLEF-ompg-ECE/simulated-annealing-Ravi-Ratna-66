# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** S.Ravi Ratna 
**Student ID    :** 2310040132  
**Date Submitted:** 23/03/2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
count_clashes() measures the total number of exam clashes in the timetable, where a clash occurs when a student has two or more exams scheduled in the same time slot. A value of 0 means a perfect timetable with no clashes.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
generate_neighbor() creates a neighboring solution by randomly selecting one exam and moving it to a different time slot. The new timetable differs from the current one by having exactly one exam reassigned to a different slot.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept the neighboring solution as the new current solution. It always accepts if the neighbor has fewer clashes (delta < 0), and probabilistically accepts worse solutions with probability exp(-delta / T). SA accepts worse solutions to allow exploration of the search space and escape local optima.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379 |
| Clashes at iteration 1 | 12 |
| Final best clashes | 3 |
| Did SA reach 0 clashes? (Yes / No) | No |

**Copy the printed timetable output here:**
```
  Final Timetable
------------------------------------------
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
------------------------------------------
  Total clashes : 3
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The plot shows the best clashes decreasing over iterations, with the temperature decreasing exponentially. The biggest drop in clashes happens in the early iterations when the temperature is high, allowing more exploration. The curve flattens out towards the end as the temperature cools and the algorithm converges to a local optimum.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        | 8             | 31                   | No                 |
| 0.95        | 3             | 135                  | No                 |
| 0.995       | 3             | 1379                 | No                 |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
Fast cooling with rate 0.80 leads to quick convergence but poorer results, as the algorithm doesn't have enough time to explore the solution space before the temperature drops too low. In contrast, slow cooling with rate 0.995 allows for more thorough exploration, resulting in better final clashes despite taking more iterations. The rate 0.95 provides a balance, achieving similar quality to 0.995 but in fewer iterations. Overall, slower cooling generally yields better optimization results in simulated annealing.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
0.95 gave the best result, achieving 3 clashes in 135 iterations. It balances exploration and exploitation effectively, allowing sufficient time to find good solutions without excessive computation.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | SA reduced clashes from 12 to 3 in 1379 iterations. |
| 2 — Cooling rate | cooling_rate = 0.95 | 3 | Slower cooling rates improve solution quality but require more iterations. |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
Simulated Annealing is a powerful optimization technique that can find good solutions to complex problems like timetable scheduling. The key insight is that accepting worse solutions probabilistically allows the algorithm to explore the search space more thoroughly and avoid getting stuck in local optima. The cooling rate parameter is critical, as slower cooling leads to better results by giving more time for exploration, but too slow can be inefficient.
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, timetable pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
