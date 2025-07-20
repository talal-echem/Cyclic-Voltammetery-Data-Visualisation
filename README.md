# Cyclic-Voltammetery-Data-Visualisation
Beautiful CV Plotting in RHE Scale with iR Correction
This Python script processes and plots Cyclic Voltammetry (CV) data exported from EC-Lab software (BioLogic) and converts the potential to RHE scale with iR correction, resulting in publication-quality graphs. It supports multiple files and allows you to select specific cycle numbers for comparison (e.g. before and after electrolysis).
# 📈 Cyclic Voltammetry Data Processor: RHE & iR-Corrected Beautiful Graphs

This repository provides a Python script to process and plot **cyclic voltammetry (CV)** data exported from **EC-Lab** (BioLogic), converting potential values from Ag/AgCl to the **RHE scale** and applying **iR correction**. It produces **high-quality plots** suitable for publications or presentations.

![Cyclic Voltammetry Graph](CV1 (2).png)
✅ Features
Supports multiple CV files (before/after electrolysis, various current densities).

Converts potential from Ag/AgCl reference to RHE scale.

Applies manual iR correction using uncompensated resistance (R) values.

Customizable cycle selection and legends.

Automatically calculates and plots current density (mA/cm²).

Clean, professional plot formatting with:

matplotlib + SciencePlots style

Axis formatting without origin tick clutter

Annotated with electrolyte information

Saves output as a high-resolution PNG figure.

📁 Input Data Format
Each CV .txt file must contain at least the following tab-separated columns exported from EC-Lab:

bash
Copy
Edit
Ewe/V    <I>/mA    cycle number
Ewe/V: Measured potential vs Ag/AgCl

<I>/mA: Current in milliamps

cycle number: Number of the voltammetry cycle

Make sure to export individual segments for multiple cycles if needed.

⚙️ Customization Parameters
Inside the script, you can configure:

python
Copy
Edit
file_paths = ['Mx1before.txt', 'mx2after.txt', 'mx4after.txt', 'mx6after.txt']
python
Copy
Edit
cycles_and_legends = {
    'Mx1before.txt': {'cycles': [2], 'legends': ['Before electrolysis'], 'R': 9},
    'mx2after.txt':  {'cycles': [2], 'legends': ['After electrolysis (25 mA/cm²)'], 'R': 8.5},
    ...
}
Also editable:

pH = 5 → for Nernst correction

iRcorrection = 95 → % compensation to apply

electrode_area = 3.87 → in cm²

📊 Output
The script will generate a file:

Copy
Edit
CV1.png
Transparent background

Styled axes and legend

RHE-corrected potential on X-axis

Current density on Y-axis

Saved at 300 dpi (for publication or slides)

🧮 Electrochemical Conversion Details
The script uses the following formula for converting to RHE and iR corrected potential:

mathematica
Copy
Edit
E (RHE-iR) = Ewe + 0.059*pH + 0.21 - R * (1 - iRcorrection/100) * I / 1000
Where:

Ewe is potential vs Ag/AgCl (in V)

R is uncompensated resistance (in ohms)

I is current (in mA)

0.21 V is the standard offset between Ag/AgCl and SHE

0.059*pH is the Nernstian pH adjustment

📦 Requirements
Install dependencies with:

bash
Copy
Edit
pip install pandas matplotlib SciencePlots
Add the science style to matplotlib using:

python
Copy
Edit
import matplotlib.pyplot as plt
plt.style.use(['science', 'notebook', 'grid'])
▶️ How to Use
Export CV data from EC-Lab as .txt (with tab separators and headers).

Place the .txt files in your working directory.

Modify the script to:

Update filenames in file_paths

Set correct R, cycle, and legend for each file

Run the script using Python.

Find your beautiful graph saved as CV1.png.

✍️ Example Plot Annotation
You can change the electrolyte label at the bottom of the figure:

python
Copy
Edit
plt.figtext(0.51, -0.1, '0.5M CA acid', ha='center', va='bottom', fontsize=16, color='blue')
📌 Notes
Data must be pre-cleaned (remove corrupted segments or overextended cycles).

This script is optimized for comparative studies (e.g., catalyst stability, electrolysis effects).

Add your institution logo or watermark if needed via plt.figimage() or fig.text().
