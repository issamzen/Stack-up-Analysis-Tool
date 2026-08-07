<div align="center">

<!-- Replace with your logo -->
<img src="CatiaStackUpTool/app_logo.png" alt="CATIA Stack-Up Dashboard" width="120"/>

# CATIA Stack-Up Dashboard

**Professional tolerance stack-up analysis for CATIA assemblies**

[![Version](https://img.shields.io/badge/version-3.7.5-blue.svg)](https://github.com/YOUR_USERNAME/catia-stackup-dashboard/releases)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-lightgrey.svg)]()
[![.NET](https://img.shields.io/badge/.NET-4.8-purple.svg)]()
[![License](https://img.shields.io/badge/license-Commercial-orange.svg)]()

*Windows desktop tool for engineers who need fast, clear tolerance stack-up results.*

</div>

---

## 📌 Overview

**CATIA Stack-Up Dashboard** performs **tolerance stack-up analysis** on CATIA assemblies — and it works **even without CATIA** for manual calculations.

- Define **stack-ups**: a chain of dimensions (contributors) that build up to a **Gap** (closing dimension).
- Import contributor names directly from **CATIA** by picking two faces — or add them **manually**.
- Compute the gap with **Worst Case**, **RSS (Root Sum Square)** and **Monte-Carlo** methods.
- Compare against a specification (Target ± tolerance) and get **Cpk**, **Yield %**, failures per million and a clear **PASS / MARGINAL / NOT OK** verdict.
- Generate a professional **Excel report** with one sheet per stack-up, including CAD section screenshots, company logo and charts.

---

## ✨ Features

| Feature | Details |
|---|---|
| 🧱 **Stack-ups** | Multiple stack-ups, one closing dimension (Gap) each |
| 👥 **Contributors** | From CATIA face-picking **or** manual entry (no CATIA needed) |
| 🧮 **Calculations** | Worst Case · RSS (σ=3/6) · Monte-Carlo (20,000 sims) · Cpk · Yield · failures per million |
| 📐 **Maillons rule** | Quadratic method (≤5 links) / Arithmetic method (>5 links) |
| 📊 **Charts** | Contribution %, Cpk vs spec, Stack diagram, Status/Recommendations, Top contributors |
| 🚦 **Status engine** | 5-tier verdict (PASS / MARGINAL / WARNING / CRITICAL / FAIL) with traffic-light colors |
| 📗 **Excel export** | Summary sheet + one sheet per stack-up, with results, charts, **own CAD screenshot** and logo (2.0 × 2.8 cm) |
| 📷 **CAD screenshots** | Per-stack-up images captured from inside CATIA and linked to that stack-up only |
| 🌡 **Thermal expansion** | Material coefficients (Metal / Plastic / custom) + ΔT |
| 🏷 **Branding** | Company logo in the app header and in the Excel reports (Professional/Company) |
| 🧪 **Trial** | 14-day free trial with limits |

---

## 🖥 System Requirements

| Item | Requirement |
|---|---|
| OS | Windows 10 / 11 (64-bit) |
| Framework | .NET Framework 4.8 |
| CATIA | Optional — any version exposing the COM interface (V5/V6), needed only for face-picking & screenshots |
| Excel | Optional for the report (2010+) — CSV fallback available |
| Disk / RAM | ~50 MB / 2 GB |

---

## 🚀 Getting Started

1. **Download** the latest release (`CATIA_StackUp_Professional_Dashboard.exe` + `app_logo.png` in the same folder).
2. **Run** the exe — a 14-day free trial starts automatically.
3. **Connect CATIA** (optional): click **Connect CATIA** and open your assembly in CATIA.
4. **Create your stack-up**:
   - Click **Add + Contributor** / **Add − Contributor** (pick two faces in CATIA), **or**
   - Click **Manual +** / **Manual −** (type name, Nominal, IT(+), IT(−) yourself — no CATIA needed).
5. **Define the requirement**: Gap Target + upper/lower tolerances (or use **Use J** / **PASS spec** helpers).
6. **Export**: click **Export Excel** → a full report is saved to your Desktop.

---

## 📸 CAD Screenshot per Stack-Up

1. Select the stack-up in the **Stackup** dropdown.
2. In CATIA, set up the view you want (zoom, rotate, section plane).
3. Capture inside CATIA: **Tools → Image → Capture…** and save the image as PNG/JPG.
4. In the tool: **Capture CAD** → OK → select the saved image file → it is **linked to that stack-up only**.
5. The button shows **✓** when the stack-up has an image; **Clear CAD** removes it.

> 💡 Quick alternative: Windows **Snipping Tool** (`Win + Shift + S`) → save PNG → select it in the tool.

---

## 💳 Editions & Licensing

| Feature | Trial | **Standard** | **Professional** | **Company** |
|---|---|---|---|---|
| Price | Free 14 days | $300/yr · $50/mo | $500/yr · $80/mo | $1500/yr · $120/mo |
| Stack-ups | 2 | 5 | Unlimited | Unlimited |
| Contributors / stack-up | 3 | 20 | Unlimited | Unlimited |
| Excel export | ❌ | ✅ (no logo) | ✅ + logo | ✅ + logo |
| Analysis charts | ❌ | ✅ | ✅ | ✅ |
| Company logo in reports | ❌ | ❌ | ✅ | ✅ |
| Machine-bound key | — | ✅ | ✅ | — |
| Seats | — | 1 | 1 | 1–250 |

**How it works:**
- Keys are cryptographically signed (HMAC-SHA256), carry the edition, expiry, customer name and **machine binding** (key works on one PC only).
- The vendor issues keys with the **License Key Generator** (separate tool, not distributed to customers).
- **Online revocation** (optional, free): a public GitHub repo hosts the revoked-key list; the tool checks it at startup + every 12 h (30-day offline grace).
- Purchase & support: **ennadisto@gmail.com**

---

## 📁 Repository Layout

```
catia-stackup-dashboard/
├── CatiaStackUpTool/            # The dashboard (what customers get)
│   ├── Program.vb               # Entry point
│   ├── MainForm.vb              # Main UI + calculations + Excel export
│   ├── LicenseCore.vb           # Key generation/validation (shared crypto)
│   ├── LicenseDialog.vb         # Buy/Activate dialog
│   └── app_logo.png             # Default company logo
├── LicenseKeyGenerator/         # Vendor-only tool (kept private!)
│   ├── GeneratorForm.vb         # Make/modify/verify/cancel keys + GitHub sync
│   └── GithubSync.vb            # GitHub API for the online revocation list
├── CATIA_StackUp_Dashboard_UserGuide.md   # Full user documentation
├── GITHUB_SETUP.md              # Free online-revocation setup (no domain)
└── LICENSE_SYSTEM_STEP0.md      # Beginner guide to the licensing system
```

> ⚠️ **The License Key Generator is for the vendor only.** Keep it in a private repo — never include it in a public distribution.

---

## 🛠 Building from Source (Visual Studio)

1. Install **Visual Studio 2022** with the **.NET desktop development** workload.
2. Open `CatiaStackUpTool.sln` (dashboard) or `LicenseKeyGenerator.sln` (generator).
3. **Build → Rebuild Solution**.
4. Output: `bin\Debug\CATIA_StackUp_Professional_Dashboard.exe`.

---

## 📚 Documentation

- **[User Guide](CATIA_StackUp_Dashboard_UserGuide.md)** — full user documentation (also available as .docx)
- **[GitHub License Setup](GITHUB_SETUP.md)** — free online revocation in ~15 minutes, no domain needed
- **[Licensing from Step 0](LICENSE_SYSTEM_STEP0.md)** — how the whole licensing system works

---

## ❓ FAQ (short)

**Do I need CATIA?** No — full manual workflow available (Manual +/− contributors).

**Can the trial be reset by reinstalling?** No — the trial start date is stored per Windows user in `%APPDATA%\CatiaStackUp`.

**Can a license be shared?** Machine-bound keys work on one PC only. Company keys support multiple seats.

**Does it work offline?** Yes. Optional online verification with a 30-day offline grace.

**Why is Excel export greyed out?** It's a licensed feature (Standard or higher).

---

## 📧 Contact & Support

**Email:** ennadisto@gmail.com

---

## ⚖️ Disclaimer

CATIA is a registered trademark of Dassault Systèmes. This tool is an **independent utility** and is not affiliated with, endorsed by, or sponsored by Dassault Systèmes.

---

<div align="center">
Made with ❤️ for engineers doing tolerance stack-ups.
</div>
