# Visual Assets Guide for MLSVA Presentation

## Overview
This guide helps you extract and prepare visualizations from the notebook for your presentation.

---

## Required Visualizations

### 1. Prediction vs Actual Plots (Priority: HIGH)
**Location in Notebook:** Section 9 (Neural Network Benchmark) and Section 10 (Classical Regression)

**What to Extract:**
- Scatter plots showing predicted vs actual Shapley values
- One plot per method (NN, RF, XGBoost, SVR, KNN, PR)
- Look for plots with diagonal line (y=x) showing perfect prediction

**Where to Use:**
- Slide 10: NN performance
- Slide 11: Tree-based methods
- Slide 12: Other methods
- Slide 16: Visualization highlights

**How to Use:**
1. Run the notebook to generate plots
2. Right-click on plot → Save image as PNG
3. Name: `prediction_vs_actual_NN.png`, `prediction_vs_actual_RF.png`, etc.
4. Insert into corresponding slides

---

### 2. Performance Comparison Bar Chart (Priority: HIGH)
**Location in Notebook:** Section 11 or results comparison section

**What to Extract:**
- Bar chart comparing R² scores across all methods
- Bar chart comparing MAE/RMSE
- Bar chart comparing training times

**Where to Use:**
- Slide 13: Comparative analysis
- Slide 21: Computational efficiency

**How to Create (if not in notebook):**
```python
import matplotlib.pyplot as plt
import numpy as np

# Example data - replace with actual values from your results
methods = ['NN', 'XGBoost', 'RF', 'SVR', 'KNN', 'PR']
r2_scores = [0.95, 0.93, 0.92, 0.87, 0.84, 0.78]

plt.figure(figsize=(10, 6))
plt.bar(methods, r2_scores, color=['#2ecc71', '#3498db', '#3498db', '#e74c3c', '#e74c3c', '#e74c3c'])
plt.ylabel('R² Score', fontsize=12)
plt.xlabel('Method', fontsize=12)
plt.title('Model Performance Comparison', fontsize=14, fontweight='bold')
plt.ylim([0, 1])
plt.grid(axis='y', alpha=0.3)
for i, v in enumerate(r2_scores):
    plt.text(i, v + 0.02, f'{v:.2f}', ha='center', fontweight='bold')
plt.tight_layout()
plt.savefig('comparison_r2_scores.png', dpi=300, bbox_inches='tight')
plt.show()
```

---

### 3. Feature Importance Plot (Priority: MEDIUM)
**Location in Notebook:** Section 10 (Classical Regression) - RF or XGBoost results

**What to Extract:**
- Horizontal bar chart of top 10-15 features
- Shows which features are most important for predictions

**Where to Use:**
- Slide 15: Feature importance analysis

**How to Extract:**
- Look for `.feature_importances_` outputs from RF or XGBoost
- If plot exists, save it
- If not, create one:

```python
import matplotlib.pyplot as plt

# Example - replace with your actual feature importances
features = ['Total Distance', 'Avg Edge Weight', 'Distance Variance', 
            'Centrality', 'Clustering Coef', 'Degree Mean']
importance = [0.25, 0.18, 0.15, 0.12, 0.10, 0.08]

plt.figure(figsize=(10, 6))
plt.barh(features, importance, color='#3498db')
plt.xlabel('Importance', fontsize=12)
plt.title('Feature Importance (Random Forest)', fontsize=14, fontweight='bold')
plt.tight_layout()
plt.savefig('feature_importance.png', dpi=300, bbox_inches='tight')
plt.show()
```

---

### 4. Learning Curves (Priority: MEDIUM)
**Location in Notebook:** Section 11 (Tuned Neural Network)

**What to Extract:**
- Training loss vs epochs
- Validation loss vs epochs
- Shows model convergence and overfitting

**Where to Use:**
- Slide 18: Hyperparameter tuning insights
- Slide 27: Technical deep dive (appendix)

---

### 5. Residual Plot (Priority: LOW)
**Location in Notebook:** May be in results analysis sections

**What to Extract:**
- Histogram of prediction errors
- Helps show error distribution

**Where to Use:**
- Slide 16: Visualization highlights
- Backup slides for detailed questions

---

### 6. Dataset Statistics (Priority: LOW)
**Location in Notebook:** Section 4 (Dataset Builders) or Section 8 (Target & Feature Analysis)

**What to Extract:**
- Distribution plots of features
- Correlation heatmaps
- Summary statistics

**Where to Use:**
- Slide 28: Dataset statistics (appendix)
- Backup slides

---

## Graphics to Create (Not in Notebook)

### 1. TSP Illustration (Priority: HIGH)
**Purpose:** Show what TSP problem looks like

**How to Create:**
- Use PowerPoint/Google Slides drawing tools
- Or use Python:

```python
import matplotlib.pyplot as plt
import numpy as np

# Create simple TSP visualization
np.random.seed(42)
n_cities = 7
x = np.random.rand(n_cities)
y = np.random.rand(n_cities)

# Create a tour (example)
tour = [0, 2, 5, 6, 3, 1, 4, 0]

plt.figure(figsize=(8, 8))
plt.scatter(x, y, s=200, c='red', zorder=3, edgecolors='black', linewidths=2)

# Draw tour
for i in range(len(tour)-1):
    plt.arrow(x[tour[i]], y[tour[i]], 
             x[tour[i+1]]-x[tour[i]], y[tour[i+1]]-y[tour[i]],
             head_width=0.03, head_length=0.02, fc='blue', ec='blue', 
             length_includes_head=True, zorder=2, linewidth=2)

# Label cities
for i in range(n_cities):
    plt.text(x[i], y[i]+0.05, f'City {i+1}', ha='center', fontsize=12, fontweight='bold')

plt.xlim(-0.1, 1.1)
plt.ylim(-0.1, 1.1)
plt.title('Traveling Salesman Problem (TSP7)', fontsize=14, fontweight='bold')
plt.axis('off')
plt.tight_layout()
plt.savefig('tsp_illustration.png', dpi=300, bbox_inches='tight', facecolor='white')
plt.show()
```

**Where to Use:** Slide 4

---

### 2. Shapley Value Concept Diagram (Priority: HIGH)
**Purpose:** Illustrate what Shapley values mean

**How to Create:**
Use PowerPoint or draw.io to create:
- Central node showing coalition
- Arrows showing contributions
- Simple 3-player example

**Example Content:**
```
Players: A, B, C
Total value with all: $100
- Without A: $60 → A contributes $40
- Without B: $75 → B contributes $25
- Without C: $85 → C contributes $15

Shapley value = average marginal contribution across all orders
```

**Where to Use:** Slide 3

---

### 3. Pipeline Flow Diagram (Priority: MEDIUM)
**Purpose:** Show end-to-end workflow

**How to Create:**
Use PowerPoint SmartArt or draw.io:

```
[TSP Instances] → [Feature Extraction] → [ML Model] → [Shapley Predictions]
                        ↓
                [Exact/MC/HMC Labels]
```

**Where to Use:** Slide 17

---

### 4. Neural Network Architecture (Priority: MEDIUM)
**Purpose:** Visualize NN structure

**How to Create:**
Use draw.io or PowerPoint:

```
Input Layer (n features)
    ↓
Hidden Layer 1 (256 neurons) + ReLU + Dropout
    ↓
Hidden Layer 2 (128 neurons) + ReLU + Dropout
    ↓
Hidden Layer 3 (64 neurons) + ReLU + Dropout
    ↓
Output Layer (1 neuron) - Linear
```

**Where to Use:** Slide 27

---

## Extraction Workflow

### Step 1: Run Notebook
```bash
# Open notebook and run all cells
jupyter notebook combined_mlsva_pipeline.ipynb

# Or convert to Python and run
jupyter nbconvert --to python combined_mlsva_pipeline.ipynb
python combined_mlsva_pipeline.py
```

### Step 2: Save Plots
For each plot you need:
1. Right-click on plot in Jupyter
2. Save Image As...
3. Choose PNG format
4. Use descriptive name
5. Save to presentation_assets/ folder

### Step 3: Create Missing Graphics
Use the Python code examples above or drawing tools to create:
- TSP illustration
- Shapley concept diagram
- Pipeline diagram
- Architecture diagram

### Step 4: Optimize for Presentation
```bash
# Optional: Optimize PNG file sizes
# Install optipng: sudo apt-get install optipng
optipng -o5 *.png

# Or use online tools like tinypng.com
```

---

## Image Specifications

### For PowerPoint/Slides:
- **Format:** PNG (supports transparency)
- **Resolution:** 300 DPI minimum
- **Size:** 1920x1080 pixels for full slide
- **Size:** 800x600 pixels for embedded plots
- **Background:** Transparent or white

### For PDF Export:
- **Format:** PNG or SVG (vector)
- **Resolution:** 300 DPI
- **Color space:** RGB

### For Print Materials:
- **Format:** PNG or PDF
- **Resolution:** 600 DPI
- **Color space:** CMYK

---

## Quick Access Template

Create a folder structure:
```
presentation_assets/
├── plots/
│   ├── prediction_vs_actual_NN.png
│   ├── prediction_vs_actual_RF.png
│   ├── comparison_r2_scores.png
│   └── feature_importance.png
├── diagrams/
│   ├── tsp_illustration.png
│   ├── shapley_concept.png
│   └── pipeline_diagram.png
└── backup/
    └── (additional plots for Q&A)
```

---

## Time-Saving Tips

1. **Batch Export:** Run notebook once, save all plots at once
2. **Name Consistently:** Use descriptive names (method_metric_dataset.png)
3. **Keep Originals:** Don't overwrite original notebook plots
4. **Version Control:** Keep separate folders for different presentations
5. **Cloud Backup:** Store in Dropbox/Drive for access anywhere

---

## Color Schemes

### Recommended Colors:
- **Success/Best:** #2ecc71 (green)
- **Good:** #3498db (blue)
- **Warning:** #f39c12 (orange)
- **Poor:** #e74c3c (red)
- **Neutral:** #95a5a6 (gray)

### For Methods:
- Neural Network: #8e44ad (purple)
- Random Forest: #27ae60 (green)
- XGBoost: #f39c12 (orange)
- SVR: #3498db (blue)
- KNN: #e74c3c (red)
- Polynomial: #95a5a6 (gray)

---

## Accessibility

Make sure visualizations are:
- **High contrast:** Readable on projector
- **Colorblind-friendly:** Use patterns or labels in addition to color
- **Large text:** Minimum 16pt font in plots
- **Simple:** Avoid clutter
- **Labeled:** Clear axis labels and legends

---

## Troubleshooting

### Plot Not Showing:
- Make sure cell is executed
- Check for errors in code
- Verify matplotlib backend

### Low Quality:
- Increase DPI: `plt.savefig('file.png', dpi=300)`
- Use larger figure size: `plt.figure(figsize=(12,8))`

### Can't Save:
- Use `plt.savefig()` instead of right-click
- Check file permissions
- Try different folder

---

## Final Checklist

Before presentation:
- [ ] All key plots extracted
- [ ] Diagrams created
- [ ] Images organized in folder
- [ ] File names are descriptive
- [ ] Quality checked (300 DPI)
- [ ] Colors are accessible
- [ ] Backup copies made

---

Good luck with your visualizations! Clear graphics make all the difference in presentations. 📊🎨
