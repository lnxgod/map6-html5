Hosted on www.charitycase.net 
Click the Tesla Logo at the top
www.charitycase.net/blank

# User Manual: JB4/Lap3 HTML Log Analyzer

This page is an all-in-one tool for analyzing JB4/Lap3 logs by:

- Parsing a CSV file (entirely client-side—no server required).  
- Running “check” functions to look for potential issues in the data (timing deviations, fuel trims, etc.).  
- Generating text-based reports summarizing warnings or anomalies.  
- Plotting multiple columns of data on a single Plotly chart with up to four Y-axes.

---

## 1. Opening the Analyzer

1. **Double-Click `index.html`**  
   Simply open it in any modern browser (Chrome, Firefox, etc.). Alternatively, if you have it hosted online (e.g., via GitHub Pages), navigate to that public URL in your browser.

2. **Check for Plotly**  
   Ensure Plotly.js and any other scripts load successfully. If something fails, open your browser’s DevTools console to check for errors.

3. **Familiarize Yourself with the Layout**  
   After the page loads, you’ll see:

   - A dashed “Drag/Drop or Click to Select CSV” area for uploading logs.  
   - 4Cyl/6Cyl sensitivity fields and a “Re-Scan Log” button.  
   - Two text regions for the “Log Length Warning” and “Report Output.”  
   - A “Plotly Multi-Axis Controls” section with four dropdowns (Axis1–Axis4) plus scale toggles (linear/log).  
   - A large chart area at the bottom.

---

## 2. Uploading Your CSV File

The page is designed to work with JB4/Lap3 logs that have ~37 columns (e.g., `timestamp`, `rpm`, `boost`, etc.). When you upload the file, it attempts to parse those columns automatically.

### 2.1 CSV Format

- The script reads lines 5 onward as data rows (some JB4 logs have 5 lines of header info).  
- If your file is too short (<10 lines total), you’ll see an error.  
- You can adapt the parsing code if your CSV differs significantly from the default JB4 format.

### 2.2 How to Upload

- **Drag & Drop**: Drag the CSV file from your file explorer onto the dashed area.  
- **Click to Browse**: Click inside the dashed area to open a file dialog, then select your CSV.

Once loaded, the script parses your CSV into an array of objects (each column is turned into a numeric field, if possible).

---

## 3. Checking the Log

### 3.1 Automatic Check

- As soon as a valid CSV is parsed, the script **immediately** runs “check” functions.  
- These checks look for timing deviation, high fuel trims, HPFP issues, meth flow problems, etc.  
- The **“Report Output”** box is populated with warnings. Sections with no findings may remain empty or only show a header.  
- The **“Log Length Warning”** box might display messages if your log doesn’t cover a sufficient speed range at wide-open throttle.

### 3.2 Sensitivity Controls

You’ll see two fields controlling thresholds for ignition checks:

- **4Cyl Sensitivity**  
- **6Cyl Sensitivity**

If you see too many false positives, **increase** them; if you suspect small deviations aren’t being caught, **decrease** them. After changing values, click **“Re-Scan Log”** to run the checks again.

### 3.3 Report Sections

- **IAT** — Looks for high IAT when throttle > 95%.  
- **HPFP Report** — Alerts if high-pressure fuel pump pressure is too low under load.  
- **Meth Flow Report** — Checks for insufficient meth flow if meth injection is active.  
- **Boost Deviations** — Checks for big differences between `boost` and `boost2`.  
- **Fuel Trims** — Warns about large separation between `trims_val` and `trims2`, or extremely high/low trims.  
- **Timing Crash** — Notes when ignition drops to zero at speed.  
- **Throttle Closure** — Detects if throttle closes while pedal remains near 100%.  
- **Timing Deviations** — Reports if ignition timing in multiple cylinders drifts beyond thresholds.

Non-empty sections appear at the top for easier visibility.

---

## 4. Plotting Data

### 4.1 Axis Dropdowns

At the bottom, there are four columns labeled **Axis1** through **Axis4**, each with a dropdown listing the CSV’s numeric columns (except `timestamp`). You can select multiple columns to plot on the same axis (e.g., `rpm` + `pedal` on Axis1, `boost` + `boost2` on Axis2, etc.). The chart updates automatically as you select.

### 4.2 Scale (Linear or Log)

Below each dropdown are radio buttons for **Linear** or **Log** scale. Choose **Log** if your data spans large ranges.

### 4.3 Hover & Interact

- **Hover** on the chart to see all parameter values at a given timestamp.  
- **Zoom & Pan** using the Plotly toolbar in the top-right corner.  
- **Export** the chart image (PNG/JPEG) via the Plotly toolbar.

---

## 5. Re-Scanning & Updating

After uploading a CSV, you can:

- Adjust sensitivity and click **“Re-Scan Log”** to re-check your data.  
- Upload a different CSV, which replaces the old data and automatically refreshes the axis dropdowns.

---

## 6. Common Issues & Tips

- **CSV Format Mismatch**: If columns differ in order or count, you might see unexpected results (zeros or missing data).  
- **CORS Errors**: Some browsers block local file references. Drag/drop typically works; otherwise, host your file or run a local HTTP server.  
- **Performance**: Very large CSVs may take a few seconds to parse. Check your console if performance is sluggish.  
- **Saving Output**: The “Report Output” is just text in the browser. To keep it, copy/paste into a document.

---

## 7. Advanced Use

- **Modifying Check Functions**: The checks are all in one HTML/JS file. You can freely adjust them to suit your needs.  
- **Hosting**: Share the analyzer by hosting it on GitHub Pages, Netlify, or any static site host. Your users just need to open the link.  
- **Embedding / iFrames**: If using a website builder like Wix, embed this page via an `<iframe>`.

---

## Summary

Using the HTML-based JB4/Lap3 Log Analyzer is straightforward:

1. **Open** the page in your browser.  
2. **Upload** (or drag/drop) your CSV.  
3. **Check** warnings in the “Report Output.”  
4. **Tune** sensitivity (4Cyl/6Cyl) and re-scan as needed.  
5. **Plot** columns on up to four Y-axes to visualize your data.

This tool quickly highlights potential issues in JB4/Lap3 logs—heat soak, fuel trim problems, timing crashes, and more—without needing a standalone server or Python environment.
