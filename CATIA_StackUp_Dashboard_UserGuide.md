# CATIA Stack-Up Dashboard
## User Guide & Help Documentation — v3.7.5

*Professional tolerance stack-up analysis for CATIA assemblies*

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [System Requirements & Installation](#2-system-requirements--installation)
3. [Licensing & Editions](#3-licensing--editions)
4. [Getting Started — First Launch](#4-getting-started--first-launch)
5. [The Interface — A Guided Tour](#5-the-interface--a-guided-tour)
6. [Core Workflow — Step by Step](#6-core-workflow--step-by-step)
7. [Understanding the Calculations](#7-understanding-the-calculations)
8. [The Gap Requirement (Specification)](#8-the-gap-requirement-specification)
9. [Analysis Charts](#9-analysis-charts)
10. [Settings](#10-settings)
11. [Excel Export](#11-excel-export)
12. [CAD Screenshots per Stack-Up](#12-cad-screenshots-per-stack-up)
13. [Logo & Branding](#13-logo--branding)
14. [RSS Demonstration Dialog](#14-rss-demonstration-dialog)
15. [Frequently Asked Questions](#15-frequently-asked-questions)
16. [Troubleshooting](#16-troubleshooting)
17. [Support & Purchasing](#17-support--purchasing)

---

## 1. Introduction

**CATIA Stack-Up Dashboard** is a Windows tool that performs **tolerance stack-up analysis** on CATIA assemblies. It lets you:

- Define **stack-ups**: a chain of dimensions (contributors) that build up to a closing dimension (the **Gap**).
- Import contributor names directly from **CATIA** by picking two faces.
- Compute the gap with **Worst-Case**, **RSS (Root Sum Square)** and **Monte-Carlo** methods.
- Compare the result against a **specification (Target ± tolerance)** and get **Cpk**, **Yield %**, failures per million and a clear **PASS / MARGINAL / NOT OK** verdict.
- Generate a professional **Excel report** with one sheet per stack-up, including CAD section screenshots and charts.

### Key concepts

| Term | Meaning |
|---|---|
| **Stack-Up** | One analysis chain. Example: *"door gap"*, *"cover to housing clearance"*. |
| **Contributor** | One dimension of the chain. Each contributor has a Nominal value, tolerances IT(+) / IT(−), and a **sign** (+ adds to the gap, − subtracts). |
| **Gap (closing dimension)** | The **result** — it is **never measured or picked**; it is *computed* from all contributors. |
| **Specification** | Your requirement: a **Target** value plus upper (+) and lower (−) tolerances → defines LSL and USL. |
| **Worst Case** | Min/max gap if every contributor is simultaneously at its extreme tolerance. |
| **RSS** | Statistical combination assuming independent, normally-distributed contributors. |
| **Cpk** | Process capability index of the computed chain vs. the specification. |
| **Yield** | % of produced assemblies expected to fall inside the specification (Monte-Carlo). |

---

## 2. System Requirements & Installation

### Requirements

| Item | Requirement |
|---|---|
| Operating system | Windows 10 / 11 (64-bit) |
| Framework | .NET Framework 4.8 (installed automatically with the tool if missing) |
| CATIA | Any version that exposes the CATIA COM interface (V5/V6 via Automation); an **open CATPart or CATProduct** must be active |
| Excel | Microsoft Excel (2010 or newer) — required for the Excel report export |
| Disk / RAM | ~50 MB disk, 2 GB RAM minimum |

### Installation

1. Run `CATIA_StackUp_Professional_Dashboard.exe` — no installer needed (portable).
2. First launch creates a **14-day free trial** automatically.
3. To make it available for all users, place the exe in a shared folder (e.g. `C:\Program Files\CATIAStackUp`) — admin rights are needed to write there for the trial file; per-user data is stored in `%APPDATA%\CatiaStackUp`.

> ⚠️ **Antivirus note:** some antivirus software may flag the exe because it automates CATIA and Excel. Add an exclusion if this happens.

---

## 3. Licensing & Editions

The tool runs as a **14-day free trial** after first launch. During the trial, some features are **locked** (see table below). To continue beyond the trial, you purchase a license from your vendor.

### Editions & prices

| Feature | Free Trial | **Standard** | **Professional** | **Company** |
|---|---|---|---|---|
| Price | — | **$300 / year** or **$50 / month** | **$500 / year** or **$80 / month** | **$1500 / year** or **$120 / month** |
| Stack-ups calculated | 2 | 5 | Unlimited | Unlimited |
| Contributors per stack-up | 3 | 20 | Unlimited | Unlimited |
| Excel export | ❌ Locked | ✅ (no company logo) | ✅ + company logo | ✅ + company logo |
| PASS spec quick-set | ❌ Locked | ✅ | ✅ | ✅ |
| Analysis charts (Contribution %, Cpk, Stack diagram, Status, Top contributors) | ❌ Locked | ✅ | ✅ | ✅ |
| Change the company logo | ❌ Locked | ✅ | ✅ | ✅ |
| Machine-bound key (anti-sharing) | — | Optional | Optional | — |
| Seats on the key | — | 1 | 1 | 1–250 |

### How to activate your license

1. Open the tool and click the orange **Buy License** button (lock icon, top-right of the window).
2. The **License & Purchase** dialog shows:
   - the three editions with prices,
   - your **Machine code** (e.g. `PC123 - john.doe`),
3. Send your **name** + **Machine code** to your vendor and tell them which edition you want.
4. The vendor sends you an **activation key** (format: `XXXXXX-XXXXXX-XXXXXX-XXXXXX`).
5. Paste the key into the dialog, enter your name, click **Activate**.
6. You get a confirmation: *"License activated successfully! Edition: … Valid until: …"* — **all features unlock immediately**, no restart needed.
7. The **Buy License** button turns green and reads **Licensed**; the status bar shows your edition and expiry date.

### Important notes about keys

- **Machine-bound keys** only work on the one PC whose machine code was used when the vendor generated the key. If you get a new PC, ask your vendor for a new key.
- **Expiry:** when a license expires, the tool falls back to trial limits automatically. Renew by asking your vendor for a new key with a later validity date.
- **Upgrade / downgrade:** simply activate the new key — the new edition's limits apply immediately.
- The license is stored in a file named `license.key` next to the exe. Do not delete it.

---

## 4. Getting Started — First Launch

1. Start **CATIA** and open the assembly (`.CATProduct`) or part you want to analyze.
2. Start the **CATIA Stack-Up Dashboard**.
3. Click **Connect CATIA** in the command bar.
   - The status pill top-left turns **CONNECTED** (green).
   - The status bar shows the connected document name.
   - The left panel fills with the **CATIA product structure**.
4. Fill in the project fields in the header: **Project**, **Number**, **Description** (they appear in the Excel report).

> If the connection fails, see [Troubleshooting](#16-troubleshooting).

---

## 5. The Interface — A Guided Tour

```
┌─────────────────────────────────────────────────────────────────────────┐
│ LOGO  CATIA Stack-Up Dashboard         CONNECTED   [Project] [Number]   │
│       AURORA • v3.7.5                              [Description]  Buy   │
├─────────────────────────────────────────────────────────────────────────┤
│ Connect CATIA │ Refresh │ New Stackup │ Add New Stackup │ Export Excel  │
│ Capture CAD │ Clear CAD │ Settings │ Buy License                        │
├──────────────┬──────────────────────────────────────────┬───────────────┤
│ CATIA Product│ Gap and Contributors                     │ Selected      │
│ Structure    │ Stackup: [combo] [Delete]                │ Contributor   │
│ (tree)       │ Gap: [Target] [+/-] Use J PASS spec      │ editor:       │
│              │ [Add +][Add -] Remove MoveUp MoveDown    │ Name, Part 1, │
│              │ KPI cards: Nominal / Worst / RSS / Cpk / │ Part No, Rev, │
│              │ Yield / Overall Status                   │ Nominal, IT+, │
│              │ Contributors grid                        │ IT-, Sign,    │
│              │ Result bar (bottom)                      │ Datum, Proc σ,│
│              │                                          │ Description   │
│              │                                          │ + Analysis    │
│              │                                          │ Charts (tabs) │
├──────────────┴──────────────────────────────────────────┴───────────────┤
│ Status bar: messages / trial days / license info / document             │
└─────────────────────────────────────────────────────────────────────────┘
```

| Zone | What it does |
|---|---|
| **Header** | Company logo (owner default), title + version, CATIA connection pill, project fields, **Buy License** button |
| **Command bar** | Connect CATIA, Refresh tree, New Stackup, Add New Stackup, Export Excel, Capture CAD, Clear CAD, Settings, Buy License |
| **Left panel** | CATIA product structure (read-only browser of the active assembly) |
| **Center panel** | Stack-up selector + Gap requirement, contributor toolbar, KPI cards, contributors grid, result bar |
| **Right panel** | Contributor editor (top) + Analysis Charts (tabs: Contribution %, Cpk, Stack Diagram, Status/Recs, Top Contrib.) |
| **Status bar** | Live messages, trial/license status, connected document |

---

## 6. Core Workflow — Step by Step

### Step 1 — Create a stack-up
- On first launch a stack-up named **Stackup 1** exists. Use **Add New Stackup** to create more (one gap per stack-up).
- Use **New Stackup** to clear everything and start over (⚠️ it deletes all stack-ups).
- Select a stack-up in the **Stackup** dropdown to switch; **Delete** removes it.

### Step 2 — Add contributors

**Option A — Manually (no CATIA needed):**
1. Click **Manual +** or **Manual −** in the contributor toolbar.
2. A new contributor row appears; the editor opens so you can type the **Name**, **Nominal 1**, **IT1(+)**, **IT1(−)** yourself.
3. Click **Apply to row**.

**Option B — From CATIA (imports part names):**
1. Click **Add + Contributor** (positive direction) or **Add − Contributor** (negative direction).
2. CATIA comes to the front. A message asks you to select **two FACES**.
3. Click the first face in the 3D view, then the second face.
4. Back in the tool, a new contributor row appears with the two part names imported.

> Only the **names** are imported. You type the Nominal and tolerances yourself. The tool works fully **without CATIA** — it is only needed for face picking and CAD screenshots.

### Step 3 — Enter the contributor values
In the grid (or via the **Selected Contributor** editor on the right):

| Field | Description |
|---|---|
| **Name** | Contributor name (default: the two picked part names) |
| **Part 1 / Part No / Rev** | Identification (imported / editable) |
| **Nominal 1** | The nominal dimension of this component (in current units). **Type a negative number to make the contributor negative.** |
| **IT1 (+)** | Upper tolerance (positive number) |
| **IT1 (−)** | Lower tolerance (positive number) |
| **Sign** | + or − (decides the direction in the chain) |
| **Datum** | Optional reference (documented in the report, not used in math) |
| **Proc. σ** | Optional real process standard deviation (mm). If empty, it is estimated from the tolerances: σ = (IT+ + IT−) / 2 ÷ sigma level |
| **Description** | Free text, exported to the report |

Click **Apply to row** (or finish editing the cell) — the results update automatically.

> 💡 Tip: you can edit cells directly in the grid. **Move Up / Move Down** reorders the chain (order matters for the report, not the math). **Remove** deletes a contributor.

### Step 4 — Define the Gap requirement (specification)
In the center panel: **Gap: [Target] [+] [−]**
- **Target**: the nominal gap you want (e.g. 0.5 mm)
- **+**: upper tolerance → USL = Target + (+)
- **−**: lower tolerance → LSL = Target − (−)

Two helpers:
- **Use J** — fills Target with the *computed* gap J and +/- with the computed gap IT. Use it when you don't know the target yet.
- **PASS spec** — sets Target = computed J and +/− = the minimum width that passes with Cpk ≥ 1.67.

> The gap itself is a **result**, never typed. Only the *requirement* is typed.

### Step 5 — Read the results
- **KPI cards**: Nominal Gap (J), Worst Case (min..max), RSS (−/+), Cpk, Yield %, Overall Status (traffic-light colors).
- **Result bar** (bottom of the grid): full summary — J, [min..max], IT(+)/IT(−), links & method, RSS, spec, Cpk, status, failures per million.
- **Analysis Charts** (right panel): see [section 9](#9-analysis-charts).

---

## 7. Understanding the Calculations

### 7.1 Gap nominal (J)
The closing dimension is the **sum of the signed contributor nominals** (thermal expansion applied if dT ≠ 0):

```
J = Σ ( signᵢ × Nominalᵢ )
```

### 7.2 Worst case
All contributors at their extreme simultaneously:

```
Gap min = J − IT(−)total        Gap max = J + IT(+)total
```

### 7.3 The maillons (links) rule
- **≤ 5 contributors (links):** quadratic method — Gap IT = arithmetic sum ÷ 2.
- **> 5 contributors:** arithmetic method — Gap IT = plain sum.

The applied method is shown in the result bar: *"Links: N (Quadratic (links <= 5))"*.

### 7.4 RSS (Root Sum Square)
Statistical combination (independent, normal contributors):

```
RSS(+) = sqrt( Σ IT(+)ᵢ² ) × sigmaFactor      sigmaFactor = 1 (σ=3) or 2 (σ=6)
RSS(−) = sqrt( Σ IT(−)ᵢ² ) × sigmaFactor
```

### 7.5 Process sigma of the chain
```
σ_chain = sqrt( Σ σᵢ² )        (σᵢ = your process sigma, or estimated from tolerances)
```

### 7.6 Cpk
```
Cpk = min( (USL − J) / (3σ), (J − LSL) / (3σ) )
```
Status thresholds (used with the spec width): **OK** if Cpk ≥ 1.33 and worst case inside spec, **MARGINAL** if 1.00–1.33, otherwise **NOT OK**.

### 7.7 Monte-Carlo & Yield
- **20,000 simulations** draw each contributor from a normal distribution (mean = nominal, σ = per contributor).
- **Yield %** = share of simulated gaps inside [LSL, USL].
- **Failures per 1,000,000** = (100 − Yield%) / 100 × 1,000,000.

### 7.8 Overall status logic (5 tiers)
`FAIL` (red) → `CRITICAL` (orange) → `WARNING` (orange) → `MARGINAL` (yellow) → `PASS` (green), based on worst-case check, RSS check, Cpk and yield. The **Status / Recs** tab explains *why* and gives recommendations.

---

## 8. The Gap Requirement (Specification)

- A requirement is "defined" as soon as you type in any of the three fields (Target, +, −).
- **Cpk / Yield / Status** need a **non-zero** spec width — if USL = LSL you'll see *"SPEC WIDTH IS ZERO"*.
- Use **Use J** to avoid guessing the target.
- Use **PASS spec** to get the minimum width that passes (Cpk ≥ 1.67).

---

## 9. Analysis Charts

Available in the **Analysis Charts** card (right panel), locked in the free trial:

| Tab | Shows |
|---|---|
| **Contribution %** | Sensitivity: each contributor's share of the total tolerance (blue: % of IT width; orange: % of IT²). The biggest bar = the driver of your stack. |
| **Cpk** | The distribution of the simulated gap (blue histogram + curve), the green specification band [LSL..USL], Cp/Cpk values and estimated % outside spec. |
| **Stack Diagram** | Visual chain: blocks for + contributors (right of 0) and − contributors (left), with the gap bracket. |
| **Status / Recs** | Verdict with icons (✔ PASS, ⚠ WARNING/MARGINAL, ✖ FAIL), all checks, messages and auto-generated recommendations. |
| **Top Contrib.** | Top 10 contributors ranked by tolerance share, color-coded by severity. |

---

## 10. Settings

Opened via **Settings** in the command bar:

| Setting | What it does |
|---|---|
| **Materials** | List of materials with thermal expansion coefficient (1/°C). Defaults: Metal 0.000012, Plastic 0.000125. Add/remove your own. |
| **Material for all parts** | Which material's coefficient is applied to every component. |
| **dT (ΔT)** | Temperature change in °C. Effective length = L × (1 + α × dT). Set 0 to ignore thermal effects. |
| **Sigma level** | 3 or 6. Scales the RSS result (×1 at σ=3, ×2 at σ=6) and the yield estimates. |
| **Units** | mm or inch. |
| **Method** | Worst + RSS (full), Worst Case only, RSS only. |
| **Company logo** | Choose / remove your own logo (locked in the free trial — see [section 13](#13-logo--branding)). |

---

## 11. Excel Export

1. Click **Export Excel**.
2. Excel opens with the workbook, saved automatically to your **Desktop** as `CATIA_StackUp_YYYYMMDD_HHMM.xlsx`.

The workbook contains:
- **Summary sheet** — project info + one row per stack-up with Nominal, Worst Case, RSS, Cpk, Yield %, Failures/1M and a **color-coded Overall Status** for every stack-up.
- **One sheet per stack-up** — parameters, the full contributors table (Part Number, Name, Rev, Nominal, tolerances, contribution %), result boxes (Nominal Stack, Worst Case +/-, 3σ RSS +/-, Summary, Overall Status badge, failures), **its own CAD screenshot**, and three charts (Monte-Carlo distribution, Tolerance contribution, Cpk vs spec). The **company logo** appears on each stack-up sheet at cells **H:I**, sized **2.0 cm × 2.8 cm** (not on the Summary sheet).

> **Free trial:** Excel export is locked — activate a license to use it.
> If Excel export fails (Excel not installed, etc.) the tool offers a **CSV fallback**.

---

## 12. CAD Screenshots per Stack-Up

Each stack-up keeps **its own** screenshot — it never mixes with another stack-up's image:

1. Select the stack-up in the **Stackup** dropdown.
2. In **CATIA**, set up the view / section exactly as you want it in the report (zoom, rotate, show the section plane).
3. Capture the image **from inside CATIA** using CATIA's own capture: **Tools → Image → Capture…** (or the capture icon), and **save the image as a file** (PNG or JPG) somewhere you can find it.
4. Click **Capture CAD** in the tool → read the message (it names the stack-up) → click **OK** → a file picker opens → **select the image you saved from CATIA**.
5. The image is now **linked to that stack-up only** (the tool shows *"CAD image linked"*).
6. The **Capture CAD** button shows **✓** when the current stack-up has an image; hover it to see the path.
7. **Clear CAD** removes the image from the current stack-up only.

> The image appears in the stack-up's own Excel sheet under *"CAD Section View – <stack-up name>"*.
>
> 💡 **Tip:** you can also use Windows' built-in **Snipping Tool** (`Win + Shift + S`) to select the 3D area and save it as a PNG — then select that file in step 4. Either way, the tool links the file you choose.

---

## 13. Logo & Branding

- **Default (owner) logo:** the tool ships with `app_logo.png` next to the exe; it is shown in the app header and in the Excel reports.
- **User logo:** licensed users can set their own logo in **Settings → Company logo** (Choose Logo… / Remove). It is stored per-user in `%APPDATA%\CatiaStackUp\logo.png` and overrides the default for that user only.
- **Free trial:** changing the logo is **locked** — trial users always see the owner's default logo.

---

## 14. RSS Demonstration Dialog

The **RSS Demo** button opens a step-by-step explanation of the RSS calculation: each contributor's IT(+)/IT(−), their squares, the sum of squares, the square root (base RSS), the sigma factor (σ/3), and the final RSS(+/-) with the gap sign swap. Useful for training and documentation.

---

## 15. Frequently Asked Questions

**Q1 — Why is the gap "0" or not computed?**
The gap is the *result* of all contributors. Add at least one contributor and enter Nominal/IT values. With no values, the result bar says *PENDING*.

**Q2 — My Cpk chart is empty.**
The Cpk chart needs tolerance data: enter IT(+) and IT(−) for each contributor (or a process sigma). With all-zero tolerances the chart shows a message instead of drawing.

**Q3 — Can I use the tool without CATIA?**
Yes — completely. Use the **Manual + / Manual −** buttons in the contributor toolbar to add contributors by typing Name, Nominal and tolerances yourself. CATIA is only needed for face picking (Add + / Add −) and for CAD screenshots (Capture CAD).

**Q4 — What happens when my trial ends?**
The tool shows a warning and opens the License dialog. Until you activate a key, it keeps working with trial limits (2 stack-ups, 3 contributors, locked export/charts/logo).

**Q5 — Can I reinstall to get a fresh trial?**
No. The trial start date is stored per Windows user in `%APPDATA%\CatiaStackUp` (and next to the exe); reinstalling to another folder does not reset it.

**Q6 — I bought a license, why is it still locked?**
The key must be **activated** (pasted in the Buy License dialog), not just copied next to the exe. If you placed `license.key` manually, restart the tool. Check the status bar for the license message.

**Q7 — Does the tool work offline?**
Yes — everything runs locally. License activation is offline (key-based).

**Q8 — Can several people share one license?**
A **Company** license supports multiple seats (1–250) via its key. **Standard/Professional** keys are single-user; if the vendor enabled machine binding, the key is tied to one PC.

---

## 16. Troubleshooting

### CATIA connection fails
- Start CATIA first and open a CATPart/CATProduct.
- Run the tool **as the same Windows user** as CATIA.
- Use the **x64** build (default) if your CATIA is 64-bit.
- Close extra CATIA sessions (multiple CNEXT processes confuse the connection).
- Click **Refresh** after connecting to reload the product tree.

### Excel export fails
- Make sure Excel is installed.
- The tool offers a **CSV fallback** — accept it to still get the data.

### Screenshot problems
- Capture **per stack-up**: select the stack-up first.
- If the capture looks wrong, adjust the CATIA view and re-capture (the old image is replaced).

### Trial / license messages
- *"Trial expired"* → contact your vendor to purchase/renew.
- *"Invalid activation key"* → check the key format (24 characters, 4×6 groups) and that a machine-bound key matches *this* PC's machine code (shown in the Buy License dialog).

### The tool won't start
- Install .NET Framework 4.8 (Windows will offer it).
- Check antivirus exclusions for the exe folder.

---

## 17. Support & Purchasing

- **Buy:** click **Buy License** in the tool — see [section 3](#3-licensing--editions) for editions & prices.
- **Price details & purchase, contact:** **ennadisto@gmail.com**
- **Machine code:** always available in the Buy License dialog — send it with your order.
- **Support:** provide your **edition**, **valid-until date** (status bar) and the exact text of any error message.

---

*CATIA Stack-Up Dashboard v3.7.5 — © AURORA. CATIA is a trademark of Dassault Systèmes. This tool is an independent utility, not affiliated with or endorsed by Dassault Systèmes.*
