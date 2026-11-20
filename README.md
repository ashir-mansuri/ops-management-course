# Operations Management course site

**Live site:** https://ashir-mansuri.github.io/ops-management-course/

## What's here

| File | What it is |
|---|---|
| `index.html` | Course home page with links to everything |
| `quality-tools.html` | Quality Tools Lab: control charts (X-bar and R, p-chart), Pareto charts and fishbone diagrams. Students type or paste their own data and see the chart, the verdict and the working. |

## How the calculations work

The Quality Tools Lab does every calculation below automatically, and shows the working under "How the limits were worked out". This section explains the same steps so students can do them by hand or in Excel. Each method finishes with a worked example that uses the example data loaded in the lab, so the numbers can be checked against the screen.

- [X-bar and R chart](#x-bar-and-r-chart-for-measurements)
- [p-chart](#p-chart-for-defectives)
- [Reading a control chart](#reading-a-control-chart)
- [Pareto chart](#pareto-chart)
- [Fishbone diagram](#fishbone-diagram)
- [Doing the same in Excel](#doing-the-same-in-excel)

### X-bar and R chart (for measurements)

Use this when you **measure** something, such as weight, length, time or temperature. You take small samples (also called subgroups) at regular times, for example 5 packets every hour.

Two charts are drawn together:

- the **X-bar chart** tracks the **average** of each sample (is the process centred in the right place?)
- the **R chart** tracks the **range** of each sample (is the spread of the process stable?)

**Symbols**

| Symbol | Meaning |
|---|---|
| n | Number of items in each sample (2 to 10) |
| k | Number of samples |
| x̄ (x-bar) | Average of one sample |
| R | Range of one sample: largest value minus smallest value |
| x̿ (x-double-bar) | Grand average: the average of all the sample averages |
| R̄ (R-bar) | Average range: the average of all the sample ranges |
| A₂, D₃, D₄ | Constants that depend only on n (see table) |

**Step 1. Work out the average and range of each sample**

```math
\bar{x} = \frac{x_1 + x_2 + \dots + x_n}{n} \qquad\qquad R = x_{\text{largest}} - x_{\text{smallest}}
```

**Step 2. Work out the grand average and the average range**

```math
\bar{\bar{x}} = \frac{\bar{x}_1 + \bar{x}_2 + \dots + \bar{x}_k}{k} \qquad\qquad \bar{R} = \frac{R_1 + R_2 + \dots + R_k}{k}
```

**Step 3. Look up A₂, D₃ and D₄ for your sample size n**

| n | A₂ | D₃ | D₄ | d₂ |
|---|---|---|---|---|
| 2 | 1.880 | 0 | 3.267 | 1.128 |
| 3 | 1.023 | 0 | 2.574 | 1.693 |
| 4 | 0.729 | 0 | 2.282 | 2.059 |
| 5 | 0.577 | 0 | 2.114 | 2.326 |
| 6 | 0.483 | 0 | 2.004 | 2.534 |
| 7 | 0.419 | 0.076 | 1.924 | 2.704 |
| 8 | 0.373 | 0.136 | 1.864 | 2.847 |
| 9 | 0.337 | 0.184 | 1.816 | 2.970 |
| 10 | 0.308 | 0.223 | 1.777 | 3.078 |

Where A₂ comes from: R̄ ÷ d₂ is an estimate of the process standard deviation (σ). Control limits sit 3 standard deviations of the sample average either side of the centre line, and the standard deviation of a sample average is σ ÷ √n. Putting these together gives A₂ = 3 ÷ (d₂ × √n). For n = 5: 3 ÷ (2.326 × 2.236) = 0.577. D₃ and D₄ do the same job for the range.

**Step 4. Work out the control limits**

X-bar chart:

```math
\text{CL} = \bar{\bar{x}} \qquad \text{UCL} = \bar{\bar{x}} + A_2\,\bar{R} \qquad \text{LCL} = \bar{\bar{x}} - A_2\,\bar{R}
```

R chart:

```math
\text{CL} = \bar{R} \qquad \text{UCL} = D_4\,\bar{R} \qquad \text{LCL} = D_3\,\bar{R}
```

**Step 5. Plot and read the charts.** Look at the R chart first. The X-bar limits are built from R̄, so if the spread is out of control, the X-bar limits can't be trusted either.

#### Worked example: packet weights

The example data in the lab is 20 samples (k = 20) of 5 packets each (n = 5), weighed in grams. The target weight is 200 g.

1. Sample 1 is 199.6, 200.7, 199.7, 199.6 and 198.7.
   - Average: (199.6 + 200.7 + 199.7 + 199.6 + 198.7) ÷ 5 = 998.3 ÷ 5 = **199.66**
   - Range: 200.7 − 198.7 = **2.0**
2. Do the same for all 20 samples. The 20 averages add up to 4,001.6 and the 20 ranges add up to 64.6.
   - Grand average x̿ = 4,001.6 ÷ 20 = **200.08**
   - Average range R̄ = 64.6 ÷ 20 = **3.23**
3. For n = 5: A₂ = 0.577, D₃ = 0, D₄ = 2.114.
4. Limits:
   - X-bar chart: UCL = 200.08 + 0.577 × 3.23 = 200.08 + 1.86 = **201.94**; LCL = 200.08 − 1.86 = **198.22**
   - R chart: UCL = 2.114 × 3.23 = **6.83**; LCL = 0 × 3.23 = **0**
5. Reading: sample 15 has an average of **202.62**, which is above the UCL of 201.94. Its range (5.5) is inside the R chart limits. So the filling machine put **more** into every packet in that sample, but the spread stayed normal. That points to a special cause, for example a setting changed for that hour. The process is **out of control** until the cause is found.

**Revising the limits.** Once the special cause for sample 15 is found and fixed, remove sample 15 and recalculate x̿, R̄ and the limits from the remaining 19 samples. Use those revised limits to monitor future production.

### p-chart (for defectives)

Use this when you **count** items as good or defective (pass/fail), for example wrong orders out of every 100 orders, or faulty bulbs out of every 200 tested.

| Symbol | Meaning |
|---|---|
| n | Number of items checked in each sample (the lab assumes the same n every time) |
| d | Number of defectives found in a sample |
| p | Proportion defective in a sample = d ÷ n |
| p̄ (p-bar) | Average proportion defective across all samples |

**Step 1. Proportion defective for each sample**

```math
p = \frac{d}{n}
```

**Step 2. Average proportion defective.** Divide the total defectives by the total items checked (not the average of the p values, although with equal n both give the same answer).

```math
\bar{p} = \frac{\text{total defectives}}{\text{total items checked}} = \frac{d_1 + d_2 + \dots + d_k}{n \times k}
```

**Step 3. Standard deviation of p**

```math
\sigma_p = \sqrt{\frac{\bar{p}\,(1 - \bar{p})}{n}}
```

**Step 4. Control limits**

```math
\text{CL} = \bar{p} \qquad \text{UCL} = \bar{p} + 3\,\sigma_p \qquad \text{LCL} = \bar{p} - 3\,\sigma_p
```

If the LCL comes out below zero, use **0**: a proportion can't be negative.

If the sample size changes from sample to sample, work out σₚ and the limits separately for each sample using its own n. The limits then go up and down along the chart. The lab only handles the equal-size case.

#### Worked example: wrong orders

The example data in the lab is 20 days (k = 20). Each day, 100 orders (n = 100) were checked for mistakes.

1. Day 1 had 4 wrong orders, so p = 4 ÷ 100 = **0.04** (4%).
2. Across all 20 days there were 106 wrong orders out of 100 × 20 = 2,000 orders.
   - p̄ = 106 ÷ 2,000 = **0.053** (5.3%)
3. σₚ = √(0.053 × 0.947 ÷ 100) = √0.000502 = **0.0224**
4. Limits:
   - UCL = 0.053 + 3 × 0.0224 = 0.053 + 0.0672 = **0.1202** (12.0%)
   - LCL = 0.053 − 0.0672 = −0.0142, which is below zero, so **LCL = 0**
5. Reading: day 10 had 14 wrong orders, so p = 0.14 (14%), which is above the UCL of 12.0%. Something unusual happened that day (a new staff member, a rush, a menu change). Every other day is inside the limits.

### Reading a control chart

The lab flags two signals. Either one means the process is **out of control**: a special cause is at work and should be investigated.

1. **A point outside the limits**: above the UCL or below the LCL.
2. **A run of 7 or more points in a row on the same side of the centre line**, even if all are inside the limits. This suggests the process average (or, on the R chart, the spread) has shifted.

Points moving up and down inside the limits with no pattern are **common-cause variation**: the normal noise of the process. Reacting to each of these points (adjusting the machine every time) usually makes things worse. Textbooks list more run rules (for example the Western Electric rules); the two above are the most widely taught.

**Control limits are not specification limits.** Control limits come from the process data (what the process actually does). Specification limits come from the customer or the design (what the product must do). A process can be in control and still make packets below the customer's minimum weight. Checking that is a separate question: process capability.

### Pareto chart

Use this to decide **which problems to fix first**. It is based on the Pareto principle, which Juran called "the vital few and the trivial many": a small number of causes usually account for most of the problems.

**Steps**

1. **Count** how many times each cause (category) happened.
2. **Sort** the causes from the largest count to the smallest. (Many textbooks put "Other" last whatever its size; the lab sorts purely by count.)
3. **Total**: add up all the counts.
4. **Share** of each cause:

   ```math
   \text{Share}\ (\%) = \frac{\text{count}}{\text{total}} \times 100
   ```

5. **Running total (cumulative %)**: add each cause's count to all the counts before it, then divide by the total.

   ```math
   \text{Cumulative}\ (\%) = \frac{\text{count of this cause} + \text{counts of all causes before it}}{\text{total}} \times 100
   ```

6. **Vital few**: go down the sorted list until the cumulative % first reaches **80% or more**. That cause and every cause above it are the vital few.
7. **Draw**: bars for the counts (left axis, from 0 to the total), and a line for the cumulative % (right axis, from 0% to 100%). Draw a dashed line at 80%.

#### Worked example: customer complaints

The example data in the lab is 105 customer complaints in one month.

| Cause | Count | Share | Cumulative count | Cumulative % |
|---|---|---|---|---|
| Long waiting time | 48 | 48 ÷ 105 = 45.7% | 48 | 45.7% |
| Cold food | 22 | 22 ÷ 105 = 21.0% | 48 + 22 = 70 | 66.7% |
| Wrong order | 15 | 15 ÷ 105 = 14.3% | 70 + 15 = 85 | **81.0%** |
| Staff behaviour | 8 | 7.6% | 93 | 88.6% |
| Dirty tables | 5 | 4.8% | 98 | 93.3% |
| Price too high | 4 | 3.8% | 102 | 97.1% |
| Other | 3 | 2.9% | 105 | 100.0% |
| **Total** | **105** | **100%** | | |

The cumulative % first passes 80% at "Wrong order" (81.0%). So the vital few are **long waiting time, cold food and wrong order**: 3 of the 7 causes make up 81% of all complaints. Fixing these three first gives the biggest improvement for the effort.

The most frequent cause isn't always the most costly. If the causes have very different costs, multiply each count by its cost and build the Pareto chart on cost instead.

### Fishbone diagram

The fishbone (Ishikawa, or cause-and-effect) diagram has no calculation. It is a structured way to list possible causes before choosing a fix, which makes it part of the **Plan** step of PDCA.

1. **Write the problem** (the effect) in the head of the fish. Make it specific and measurable: "Customers wait more than 10 minutes for their order", not "Service is bad".
2. **Choose the categories** for the bones.
   - Manufacturing (6M): Manpower, Machine, Method, Material, Measurement, Environment (Mother Nature)
   - Restaurant or service: People, Process, Equipment, Materials, Place, Measurement
3. **Brainstorm causes** under each bone. For each cause, keep asking "why?" (the 5 Whys) until you reach something the team can act on.
4. **Mark the likely root causes** (in the lab, start the line with `*` and it turns red).
5. **Check them with data** before acting, for example with a check sheet or a Pareto chart of how often each cause actually happens.

### Doing the same in Excel

Put each sample on its own row, with the 5 values in columns B to F (rows 2 to 21).

| What | Formula (row 2) |
|---|---|
| Sample average | `=AVERAGE(B2:F2)` in G2, copied down |
| Sample range | `=MAX(B2:F2)-MIN(B2:F2)` in H2, copied down |
| Grand average x̿ | `=AVERAGE(G2:G21)` in J2 |
| Average range R̄ | `=AVERAGE(H2:H21)` in J3 |
| UCL for X-bar | `=J2+0.577*J3` |
| LCL for X-bar | `=J2-0.577*J3` |
| UCL for R | `=2.114*J3` |
| LCL for R | `=0*J3` |

0.577, 2.114 and 0 are A₂, D₄ and D₃ for n = 5. Swap in the values from the table for other sample sizes.

For a p-chart, with defectives in column B (rows 2 to 21) and the sample size n in E1:

| What | Formula |
|---|---|
| Proportion defective | `=B2/$E$1` in C2, copied down |
| p̄ | `=SUM(B2:B21)/($E$1*COUNT(B2:B21))` in E2 |
| σₚ | `=SQRT(E2*(1-E2)/$E$1)` in E3 |
| UCL | `=E2+3*E3` |
| LCL | `=MAX(0,E2-3*E3)` |

For a Pareto chart, with causes in A2:A8 and counts in B2:B8 (already sorted largest first):

| What | Formula (row 2) |
|---|---|
| Share | `=B2/SUM($B$2:$B$8)` copied down, formatted as % |
| Cumulative % | `=SUM($B$2:B2)/SUM($B$2:$B$8)` copied down, formatted as % |

## Using it in class

- Students can open the same link on their phones.
- Every chart can be downloaded as a PNG for assignments and slides.

## Privacy

Everything runs in the browser. Nothing typed into the tools is saved or sent anywhere. 

## Updating

All files sit at the top level (no folders). To update a page, upload the new file on github.com with the same name; the site refreshes within a few minutes.
