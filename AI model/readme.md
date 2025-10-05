# Universal Metabolic Diagnostic System

## 🧬 Overview

The **Universal Metabolic Diagnostic System** is an AI-powered tool that automates the diagnosis of **Inborn Errors of Metabolism (IEMs)** - rare genetic disorders caused by enzyme deficiencies. These conditions affect 1 in 1,000-2,500 newborns and can lead to severe disabilities or death if not diagnosed early.

### The Problem It Solves

**Challenges in IEM Diagnosis:**
- **Delayed diagnosis**: IEMs are rare, and symptoms often mimic common conditions, leading to misdiagnosis
- **Complex interpretation**: Lab reports require specialized metabolic expertise that's scarce
- **Limited access**: Many regions lack metabolic specialists, causing diagnostic delays of months or years
- **High mortality**: Without early detection, metabolic crises can be fatal
- **Family burden**: Parents struggle to get answers while their child's condition worsens

**What This System Does:**
- Analyzes lab report images using AI to identify metabolic abnormalities
- Identifies deficient enzymes and associated genes
- Fetches 3D protein structures from AlphaFold database
- Generates comprehensive genetic reports with disease associations
- Provides interactive 3D visualizations of affected proteins
- Predicts potential disabilities and complications
- Recommends confirmatory tests and treatment approaches

---

## ✨ Key Features

1. **AI-Powered Lab Report Analysis**: Upload lab images (blood/urine tests) for instant metabolic screening
2. **Protein Structure Visualization**: Auto-fetches 3D structures from AlphaFold and displays them interactively
3. **Comprehensive Genetic Reports**: HTML reports with DNA defects, inheritance patterns, and disability predictions
4. **Multi-Angle Protein Rendering**: Generates front, side, back, and top views of protein structures
5. **Web Search Integration**: Fetches latest research on identified genetic disorders (requires LLM.py)
6. **Interactive Web Viewer**: Browser-based 3D viewer with molecular graphics
7. **URL Support**: Download and analyze lab reports directly from URLs
8. **Clinical Decision Support**: Provides urgency assessment and treatment recommendations

---

## 🚀 Quick Start

### Prerequisites

```bash
pip install pillow requests
```

**Optional (for web search capabilities):**
- Place `LLM.py` in the same directory (enables latest research lookup)

### Step 1: Get Your API Key

⚠️ **IMPORTANT**: The system uses OpenRouter AI for analysis. If the embedded API key fails:

1. Visit [OpenRouter](https://openrouter.ai/)
2. Sign in and generate a new API key
3. Replace the key in the script (line 29):
   ```python
   OPENROUTER_API_KEY = "sk-or-v1-YOUR_NEW_KEY_HERE"
   ```

### Step 2: Run the Script

```bash
python med3.py
```

### Step 3: Follow the Prompts

```
Enter input mode ('file' or 'url'): file
Enter the path to the image file: lab_report.jpg
Enter patient details:
Age (e.g., '6 months'): 6 months
Sex (male/female): male
Symptoms (comma-separated): vomiting, lethargy, poor feeding
Family history: consanguineous parents
Clinical notes: metabolic acidosis suspected
Perform deep analysis? (yes/no): yes
```

### Step 4: Wait for Processing

The system will:
1. Analyze the lab report image
2. Extract protein IDs (e.g., P12345)
3. Download 3D structures from AlphaFold
4. Generate visualization scripts
5. Create structure images
6. Perform AI analysis on protein structures
7. Search the web for disease information
8. Generate comprehensive reports
9. Launch interactive web viewer

---

## 📂 Understanding the Generated Files

### Directory Structure

```
├── imput/                          # Input lab images
├── protein_structures/             # Downloaded PDB files
│   └── P12345_alphafold.pdb
├── visualizations/                 # PyMOL/ChimeraX scripts
│   ├── P12345_pymol.pml
│   └── P12345_chimerax.cxc
├── protein_analysis/               # Per-protein analysis
│   └── P12345/
│       ├── P12345_front.png
│       ├── P12345_side.png
│       ├── P12345_back.png
│       ├── P12345_top.png
│       └── P12345_analysis.json
├── diagnostic_results/             # Main diagnostic report
│   ├── diagnostic_report.json
│   └── viewer.html                 # Interactive 3D viewer
└── genetic_reports/                # Comprehensive reports
    └── report_TIMESTAMP/
        ├── comprehensive_genetic_report.html
        └── comprehensive_report.json
```

---

## 📊 File Descriptions

### 1. **diagnostic_report.json**
**Location:** `diagnostic_results/`

Contains the initial AI diagnosis with:
- Patient information
- Lab analysis results
- Identified protein IDs (UniProt)
- List of deficient enzymes
- Recommended confirmatory tests

**Example content:**
```json
{
  "patient_info": {
    "age": "6 months",
    "sex": "male",
    "symptoms": "vomiting, lethargy, poor feeding"
  },
  "uniprot_ids": ["P12345", "Q67890"],
  "diagnosis": "Suspected metabolic disorder...",
  "timestamp": "2025-10-05 14:30:00"
}
```

### 2. **viewer.html**
**Location:** `diagnostic_results/`

Interactive web interface featuring:
- 3D protein structure viewer (powered by 3Dmol.js)
- Patient dashboard with stats
- Lab image gallery
- Protein selection sidebar
- Style controls (cartoon/stick/sphere)
- Screenshot download capability

**How to Use:**
- Click on any protein card to load its 3D structure
- Use mouse to rotate (drag), zoom (scroll), pan (right-click drag)
- Click "Style" to toggle between cartoon/stick/sphere representations
- Click "Save" to download structure as PNG
- Click "Generate Full Report" to create comprehensive genetic report

### 3. **comprehensive_genetic_report.html**
**Location:** `genetic_reports/report_TIMESTAMP/`

Full medical report including:
- **Patient Information Section**: Demographics and clinical notes
- **DNA & Genetic Analysis**: Types of mutations detected
  - Point mutations
  - Deletions
  - Insertions
  - Splice site mutations
  - Missense mutations
  - Nonsense mutations
- **Inheritance Patterns**: Autosomal recessive/dominant, X-linked analysis
- **Initial AI Diagnosis**: Raw diagnostic output from lab image analysis
- **Protein Structure & Disease Analysis**: For each protein:
  - AI structural analysis
  - Web research findings
  - Multi-angle structure images
- **Identified Diseases & Conditions**: List of suspected disorders with clinical urgency
- **Potential Disabilities & Complications**:
  - Physical disabilities (developmental delays, motor impairments, organ dysfunction)
  - Cognitive/neurological disabilities (intellectual disability, seizures)
  - Long-term complications (metabolic crises, organ damage)
- **Conclusion & Recommendations**: Treatment plan, prognosis, next steps

### 4. **Protein Structure Images**
**Location:** `protein_analysis/PROTEIN_ID/`

Four PNG images per protein:
- `PROTEIN_ID_front.png`: Front view of 3D structure
- `PROTEIN_ID_side.png`: 90° rotated side view
- `PROTEIN_ID_back.png`: 180° rotated back view
- `PROTEIN_ID_top.png`: Top-down view

These are generated by parsing PDB atomic coordinates and rendering with depth-based coloring (blue=front, red=back).

### 5. **PDB Structure Files**
**Location:** `protein_structures/`

AlphaFold predicted protein structures in PDB format. These are fetched from the European Bioinformatics Institute (EBI) AlphaFold database.

**Example:** `P12345_alphafold.pdb`
- Contains 3D coordinates of all atoms in the protein
- Used for visualization and structural analysis
- Can be opened in PyMOL, ChimeraX, or other molecular viewers

### 6. **Visualization Scripts**
**Location:** `visualizations/`

- **PyMOL scripts (.pml)**: For professional structure rendering
- **ChimeraX scripts (.cxc)**: Alternative high-quality visualization

These can be loaded in PyMOL/ChimeraX for publication-quality images.

### 7. **comprehensive_report.json**
**Location:** `genetic_reports/report_TIMESTAMP/`

Machine-readable version of the comprehensive report containing:
```json
{
  "timestamp": "2025-10-05T14:30:00",
  "patient_info": {...},
  "diagnosis": "...",
  "uniprot_ids": ["P12345", "Q67890"],
  "protein_analyses": {...},
  "dna_defect_types": [...],
  "potential_disabilities": {
    "physical": [...],
    "cognitive": [...],
    "complications": [...]
  }
}
```

---

## 🎯 How to Visualize Results

### Method 1: Browser-Based Viewer (Easiest)

1. The script automatically opens `viewer.html` in your browser
2. If not, manually open: `http://localhost:8000/diagnostic_results/viewer.html`
3. Click any protein to view its 3D structure
4. Interact with the molecule using your mouse:
   - **Left-click + drag**: Rotate
   - **Scroll wheel**: Zoom in/out
   - **Right-click + drag**: Pan

### Method 2: View Comprehensive Report

1. Navigate to `genetic_reports/report_TIMESTAMP/`
2. Open `comprehensive_genetic_report.html` in any browser
3. This report auto-opens after deep analysis completes
4. Contains all clinical information, protein analyses, and recommendations

### Method 3: Professional Visualization (Advanced)

If you have PyMOL or ChimeraX installed:

```bash
# PyMOL
pymol visualizations/P12345_pymol.pml

# ChimeraX
chimerax visualizations/P12345_chimerax.cxc
```

### Method 4: View Individual Protein Reports

```bash
# Open protein-specific analysis
cat protein_analysis/P12345/P12345_analysis.json
```

---

## 🔧 Terminal Output Explained

When you run the script, you'll see:

```
======================================================================
🧬 UNIVERSAL METABOLIC DIAGNOSTIC SYSTEM
   Enhanced with Comprehensive Genetic Reporting
======================================================================

📊 STEP 1: Analyzing Lab Report
----------------------------------------------------------------------
🧠 Analyzing lab report with AI...
✅ Lab analysis complete

🔍 STEP 2: Extracting Protein Identifiers
----------------------------------------------------------------------
✅ Found 3 proteins: P12345, Q67890, P54321

🧬 STEP 3: Fetching Protein Structures
----------------------------------------------------------------------
  🔍 Fetching structure for P12345...
  ✅ P12345 → Phenylalanine hydroxylase (PAH)
  🔍 Fetching structure for Q67890...
  ✅ Q67890 → Ornithine transcarbamylase (OTC)
✅ Downloaded 2/3 structures

🎨 STEP 4: Generating Visualization Scripts
----------------------------------------------------------------------
  ✅ Scripts for P12345
  ✅ Scripts for Q67890

💾 STEP 5: Saving Diagnostic Report
----------------------------------------------------------------------
✅ Report: diagnostic_results/diagnostic_report.json

🌐 STEP 6: Generating Enhanced Web Viewer
----------------------------------------------------------------------
✅ Viewer: diagnostic_results/viewer.html

🚀 STEP 7: Starting Web Server
----------------------------------------------------------------------
✅ Server running at: http://localhost:8000

🔬 STEP 8: Deep Protein Structure Analysis
----------------------------------------------------------------------
======================================================================
Analyzing Protein 1/2: P12345
======================================================================
  📸 Generating structure images...
  📸 Created front view: protein_analysis/P12345/P12345_front.png
  📸 Created side view: protein_analysis/P12345/P12345_side.png
  📸 Created back view: protein_analysis/P12345/P12345_back.png
  📸 Created top view: protein_analysis/P12345/P12345_top.png
  ✅ Generated 4 images

  🧠 AI analysis of structure images...
  🔬 Analyzing P12345 structure from 4 angles...
  ✅ AI structural analysis complete

  🌐 Searching web for disease information...
  🌐 Searching web for: Phenylalanine hydroxylase P12345 genetic disease...
  ✅ Web search complete

  ✅ Complete analysis saved for P12345

======================================================================
Analyzing Protein 2/2: Q67890
======================================================================
  [Similar process repeats]

======================================================================
✅ PROTEIN ANALYSIS COMPLETE
======================================================================

📊 STEP 9: Generating Comprehensive Genetic Report
----------------------------------------------------------------------
======================================================================
🧬 GENERATING COMPREHENSIVE GENETIC REPORT
======================================================================
✅ HTML Report: genetic_reports/report_1234567890/comprehensive_genetic_report.html
✅ JSON Report: genetic_reports/report_1234567890/comprehensive_report.json
======================================================================

🌐 STEP 10: Launching Interactive Viewer
----------------------------------------------------------------------
✅ Opening browser: http://localhost:8000/diagnostic_results/viewer.html

======================================================================
✅ DIAGNOSTIC PIPELINE COMPLETE
======================================================================
📊 Proteins: 2
🧬 Structures: 2
🎨 Scripts: 4
🌐 Viewer: http://localhost:8000/diagnostic_results/viewer.html
📄 Reports: genetic_reports
======================================================================

⚠️  Press Ctrl+C to stop server
```

**What Each Step Does:**

1. **Lab Report Analysis**: AI examines the image to identify abnormal metabolic markers
2. **Protein Extraction**: Finds UniProt IDs (e.g., P12345) mentioned in the diagnosis
3. **Structure Fetching**: Downloads 3D structures from AlphaFold database
4. **Script Generation**: Creates PyMOL/ChimeraX scripts for advanced visualization
5. **Report Saving**: Stores initial diagnostic data as JSON
6. **Web Viewer**: Creates interactive HTML interface
7. **Server Start**: Launches local web server on port 8000
8. **Deep Analysis**: Analyzes each protein structure from multiple angles
9. **Comprehensive Report**: Generates full clinical report with genetic insights
10. **Browser Launch**: Opens the viewer and reports in your default browser

---

## 🩺 Clinical Use Case Example

### Scenario

**Patient:** 6-month-old male infant

**Presenting Symptoms:**
- Persistent vomiting
- Lethargy
- Poor feeding
- Developmental delays

**Lab Results:**
- Elevated blood ammonia: 250 µmol/L (normal: 10-50)
- Metabolic acidosis
- Elevated orotic acid in urine

### System Analysis

**Input:**
```
Age: 6 months
Sex: male
Symptoms: vomiting, lethargy, poor feeding
Family history: consanguineous parents
Clinical notes: hyperammonemia, metabolic acidosis
```

**System Output:**

1. **Initial Diagnosis**:
   - Suspected Urea Cycle Disorder
   - Most likely: Ornithine Transcarbamylase (OTC) Deficiency

2. **Protein Identified**: Q67890 (OTC enzyme)

3. **Genetic Basis**:
   - Gene: OTC (Xp21.1)
   - Inheritance: X-linked recessive
   - Common mutations: R141Q, R129H

4. **Structural Analysis**:
   - Active site disruption visible in 3D structure
   - Substrate binding pocket malformed
   - Reduced enzyme activity predicted

5. **Predicted Complications**:
   - **Immediate**: Hyperammonemic crisis (life-threatening)
   - **Short-term**: Brain damage if untreated
   - **Long-term**: 
     - Intellectual disability
     - Developmental delays
     - Seizure disorder
     - Behavioral problems

6. **Clinical Recommendations**:
   - **URGENT**: Initiate low-protein diet immediately
   - Start ammonia scavenger therapy (sodium benzoate/phenylbutyrate)
   - Genetic sequencing for OTC gene confirmation
   - Family carrier testing (mother and siblings)
   - Consider liver transplant consultation

7. **Prognosis**:
   - With early treatment: Good control possible
   - Without treatment: High mortality risk
   - Long-term: Requires lifelong dietary management

---

## ⚠️ Important Notes

### API Key Issues

If you see errors like:
```
API Error (401): Unauthorized
```

**Solution:**

1. The embedded API key has expired or rate-limited
2. Go to [OpenRouter](https://openrouter.ai/)
3. Sign in (free account available)
4. Navigate to **Keys** → **Create Key**
5. Copy the key (starts with `sk-or-v1-`)
6. Open `med3.py` in a text editor
7. Find line 29:
   ```python
   OPENROUTER_API_KEY = "sk-or-v1-OLD_KEY_HERE"
   ```
8. Replace with your new key:
   ```python
   OPENROUTER_API_KEY = "sk-or-v1-YOUR_NEW_KEY_HERE"
   ```
9. Save and re-run the script

### Web Search (Optional)

The `LLM.py` module enables fetching latest research on genetic disorders.

**With LLM.py:**
```
✅ LLM.py loaded - Web search enabled
```

**Without LLM.py:**
```
⚠️  LLM.py not found - Web search disabled
```

The system still works without it, but web research sections will show "Web search not available."

### Browser Compatibility

The 3D viewer works best in:
- ✅ Chrome/Edge (recommended)
- ✅ Firefox
- ✅ Safari
- ❌ Internet Explorer (not supported)

### Port Conflicts

If port 8000 is already in use:
```python
# Edit the port number in med3.py
port = 8001  # Change to any available port
```

### Large Lab Images

For high-resolution images, the upload may take longer. Be patient during Step 1.

### No Proteins Found

If the AI doesn't find any UniProt IDs:
- Check if the lab report image is clear and readable
- Ensure the report contains metabolic markers
- Try a different image or manual input

---

## 🔍 Understanding the Code

### Main Components

**1. Configuration (Lines 18-30)**
```python
OPENROUTER_API_KEY = "..."  # AI analysis API key
STRUCTURE_DIR = "protein_structures"  # PDB files
VISUALIZATION_DIR = "visualizations"  # Scripts
RESULTS_DIR = "diagnostic_results"  # Main reports
```

**2. File Download (Lines 32-64)**
- `download_file_from_url()`: Fetches lab reports from URLs
- Supports images, PDFs, genetic data files

**3. AI Analysis (Lines 66-197)**
- `analyze_lab_image()`: Sends image to AI for metabolic screening
- `analyze_protein_structure_images()`: Analyzes 3D structures for defects
- `web_search_protein_diseases()`: Fetches latest research (requires LLM.py)

**4. Report Generation (Lines 199-436)**
- `generate_comprehensive_genetic_report()`: Creates full HTML/JSON reports
- Includes DNA analysis, disabilities, treatment recommendations

**5. Protein Functions (Lines 438-570)**
- `extract_uniprot_ids()`: Finds protein IDs in text (e.g., P12345)
- `fetch_protein_structure()`: Downloads from AlphaFold
- `generate_pymol_script()`: Creates visualization scripts

**6. Image Generation (Lines 572-743)**
- `create_protein_structure_visualization()`: Renders multi-angle images
- Parses PDB coordinates and applies 3D rotations
- Depth-based coloring (blue=front, red=back)

**7. Web Viewer (Lines 745-1020)**
- `generate_enhanced_web_viewer()`: Creates interactive HTML interface
- Embeds 3Dmol.js for molecular graphics
- Patient dashboard and analysis panels

**8. Advanced Analysis (Lines 1022-1115)**
- `analyze_all_proteins()`: Runs deep analysis on all identified proteins
- Combines AI + web search + structure visualization

**9. Main Pipeline (Lines 1117-1296)**
- `run_complete_diagnostic_pipeline()`: Orchestrates entire workflow
- Handles user input, processing, report generation, viewer launch

---

## 🧪 Example Lab Reports

The system can analyze various lab test formats:

### Blood Tests
- Complete Blood Count (CBC)
- Comprehensive Metabolic Panel (CMP)
- Amino Acid Analysis
- Acylcarnitine Profile
- Organic Acid Analysis

### Urine Tests
- Amino Acid Screen
- Organic Acid Screen
- Urea Cycle Metabolites

### Genetic Tests
- DNA Sequencing Results
- Chromosome Analysis
- Gene Panel Reports

---

## 🔬 Supported Metabolic Disorders

The system can help diagnose:

- **Amino Acid Disorders**: PKU, Maple Syrup Urine Disease, Homocystinuria
- **Organic Acidemias**: Methylmalonic Acidemia, Propionic Acidemia
- **Urea Cycle Disorders**: OTC Deficiency, Citrullinemia, Argininosuccinic Aciduria
- **Fatty Acid Oxidation Defects**: MCAD, LCHAD, VLCAD deficiencies
- **Carbohydrate Disorders**: Galactosemia, Glycogen Storage Diseases
- **Mitochondrial Disorders**: Respiratory chain defects
- **Lysosomal Storage Diseases**: Gaucher, Fabry, Pompe diseases

---

## 📚 Technical Details

### AI Model
- **Provider**: OpenRouter
- **Model**: Google Gemma 3 27B
- **Capabilities**: Multimodal (text + images)

### Protein Database
- **Source**: AlphaFold Database (EBI)
- **Coverage**: 200+ million protein structures
- **Quality**: Experimental + AI-predicted structures

### Visualization
- **Frontend**: 3Dmol.js (WebGL-based)
- **Backend**: PIL (Python Imaging Library)
- **Professional**: PyMOL/ChimeraX script generation

### Web Server
- **Framework**: Python built-in HTTPServer
- **Port**: 8000 (configurable)
- **Threading**: Daemon thread for non-blocking

---

## 🛠️ Troubleshooting

### Issue: "No module named 'PIL'"
**Solution:**
```bash
pip install pillow
```

### Issue: "No proteins found in diagnosis"
**Possible causes:**
1. Lab report doesn't contain metabolic markers
2. Image quality too low
3. AI didn't identify abnormalities

**Solution:** Try a clearer image or one with more obvious metabolic abnormalities

### Issue: "Structure not available for protein X"
**Explanation:** Not all proteins have AlphaFold structures

**Solution:** The system continues with available structures

### Issue: Browser doesn't open automatically
**Solution:** Manually open:
```
http://localhost:8000/diagnostic_results/viewer.html
```

### Issue: 3D viewer shows black screen
**Possible causes:**
1. Browser doesn't support WebGL
2. Graphics drivers outdated

**Solution:** 
- Update browser
- Enable hardware acceleration
- Try a different browser (Chrome recommended)

---

## 📖 Additional Resources

### Learning More About IEMs
- [NORD - National Organization for Rare Disorders](https://rarediseases.org/)
- [OMIM - Online Mendelian Inheritance in Man](https://www.omim.org/)
- [Orphanet - Rare Disease Database](https://www.orpha.net/)

### Protein Structure Resources
- [AlphaFold Database](https://alphafold.ebi.ac.uk/)
- [UniProt - Protein Database](https://www.uniprot.org/)
- [PDB - Protein Data Bank](https://www.rcsb.org/)

### Molecular Visualization
- [PyMOL](https://pymol.org/)
- [UCSF ChimeraX](https://www.cgl.ucsf.edu/chimerax/)
- [3Dmol.js Documentation](https://3dmol.csb.pitt.edu/)

---

## 🤝 Contributing

This is an open-source project aimed at improving access to metabolic disorder diagnosis.

**Ways to contribute:**
- Report bugs and issues
- Suggest new features
- Improve documentation
- Add support for more lab test formats
- Enhance AI analysis prompts
- Contribute to protein structure visualization

---

## ⚖️ Disclaimer

**⚠️ IMPORTANT MEDICAL DISCLAIMER ⚠️**

This tool is designed for **research and educational purposes only**. It is NOT a substitute for professional medical diagnosis, advice, or treatment.

**Key Points:**
- Always consult qualified healthcare professionals for medical decisions
- Results are AI-generated predictions and may contain errors
- False positives and false negatives are possible
- Clinical confirmation is required for any suspected diagnosis
- Treatment should only be initiated by licensed medical practitioners
- In emergencies, seek immediate medical attention

**Legal Notice:**
- The developers assume no liability for medical decisions based on this tool
- Users are responsible for verifying all results with medical professionals
- This tool does not establish a doctor-patient relationship

---

## 📧 Support

For technical issues, questions, or feedback:
- Open an issue on the project repository
- Check existing issues for solutions
- Provide detailed error messages and screenshots

---

## 📄 License

This project is released under the MIT License for educational and research purposes.

---

## 🌟 Acknowledgments

- **AlphaFold Team** for revolutionary protein structure predictions
- **OpenRouter** for accessible AI model APIs
- **3Dmol.js** for browser-based molecular visualization
- **Medical community** for inspiring better diagnostic tools

---

**Made with care for improving rare disease diagnosis worldwide**

**Version:** 1.0.0  
**Last Updated:** October 2025  
**Status:** Active Development