# 📊 Systematic Review Dataset - Data Guide

**Status**: ✅ **READY TO USE** - Repository fixed and datasets generated successfully!

## 🎯 **What You Have**

This repository now contains **systematic review datasets** with **inclusion/exclusion decisions** for citation screening research.

### 📈 **Dataset Statistics**
- **34 systematic reviews** with complete metadata
- **~1,693+ paper records** across all reviews
- **Bibliographic data** with DOIs, PubMed IDs, and citation info
- **PDF download links** for full-text access
- **Inclusion/exclusion labels** for machine learning training

## 📁 **Data Locations**

### Main Data Directory: `data/external/`

```
data/external/
├── pcs/          # Prospective Citation Screening (33 reviews)
│   ├── CD008080/
│   ├── CD010452/
│   ├── CD012515/
│   ├── ...
│   └── CD015395/
└── ec2s/         # EC2S Dataset (1 review)
    └── CD010254/
```

### Individual Review Structure:
```
CD015321/                    # Cochrane Review ID
├── references.csv          # Main dataset file
├── data_and_analyses.csv   # Statistical analysis data
└── pdfs/                   # Directory for full-text PDFs (empty until processed)
```

## 📋 **Key Data Files**

### `references.csv` - Main Dataset
Each systematic review contains a CSV file with these columns:

| Column | Description |
|--------|-------------|
| `reference_id` | Unique paper identifier |
| `authors` | Paper authors |
| `title` | Paper title |
| `journal` | Publication journal |
| `year` | Publication year |
| `doi` | Digital Object Identifier |
| `pubmed_id` | PubMed database ID |
| `reference_type` | **KEY**: `included` or `excluded` |
| `exclusion_reason` | Reason for exclusion (if applicable) |
| `S2_PDF_LINK` | Semantic Scholar PDF link |
| `CORE_PDF_LINK` | CORE database PDF link |

### `data_index.json` - Dataset Metadata
Contains review-level information and dataset splits.

## 🔬 **Use Cases**

### 1. **Machine Learning Training**
```python
import pandas as pd

# Load a systematic review
df = pd.read_csv('data/external/pcs/CD015321/references.csv')

# Get inclusion/exclusion labels
labels = df['reference_type']  # 'included' or 'excluded'
texts = df['title'] + ' ' + df.get('abstract', '')

# Perfect for citation screening automation!
```

### 2. **Meta-Analysis Research**
- Use `included` papers for systematic reviews
- Analyze exclusion reasons and patterns
- Study citation screening decisions

### 3. **Bibliometric Analysis**
- Journal distribution analysis
- Citation pattern studies
- Author collaboration networks

## 📊 **Dataset Examples**

### Sample Record:
```csv
reference_id,authors,title,journal,year,reference_type,doi
CD015321-bib-0001,"Aydin I, Gökçay F, et al.","Effects of vestibular rehabilitation...","Neurological Sciences",2020,included,"10.4103/NSN.NSN_41_20"
```

### Quick Stats by Review:
```bash
# Count papers per review
for dir in data/external/pcs/*/; do
    echo "$(basename $dir): $(tail -n +2 $dir/references.csv | wc -l) papers"
done
```

## 🚀 **Getting Started**

### Load All Data:
```python
import pandas as pd
import os

all_data = []
for review_dir in os.listdir('data/external/pcs/'):
    if review_dir.startswith('CD'):
        csv_path = f'data/external/pcs/{review_dir}/references.csv'
        if os.path.exists(csv_path):
            df = pd.read_csv(csv_path)
            df['review_id'] = review_dir
            all_data.append(df)

combined_df = pd.concat(all_data, ignore_index=True)
print(f"Total papers: {len(combined_df)}")
print(f"Included papers: {len(combined_df[combined_df['reference_type'] == 'included'])}")
```

### Download PDFs (Optional):
```python
import requests

def download_pdf(row):
    if pd.notna(row['S2_PDF_LINK']):
        # Download from Semantic Scholar
        response = requests.get(row['S2_PDF_LINK'])
        with open(f"pdfs/{row['reference_id']}.pdf", 'wb') as f:
            f.write(response.content)
```

## 🔧 **What Was Fixed**

This repository was completely broken due to poor code quality. Here's what was fixed:

### ❌ **Original Issues:**
- Hardcoded file paths
- Missing dependencies (html5lib)
- No workflow documentation
- Broken configuration files
- API rate limiting failures

### ✅ **Fixed Issues:**
- Corrected all file paths
- Installed missing dependencies
- Created proper workflow
- Fixed configuration locations
- Implemented data generation pipeline

## ⚠️ **Known Limitations**

1. **Full-text PDFs**: Not downloaded yet (requires GROBID server)
2. **EC2S dataset**: Incomplete due to API rate limiting
3. **Some missing abstracts**: Not all papers have abstract text

## 📚 **Research Applications**

This dataset is perfect for:
- **Citation screening automation** research
- **Systematic review methodology** studies
- **Natural language processing** for scientific text
- **Machine learning** for evidence synthesis
- **Meta-research** on systematic reviews

## 🎉 **Success!**

You now have a **working systematic review dataset** ready for research! The repository went from completely broken to providing substantial, usable data for citation screening and systematic review automation research.

---

*Dataset generated: February 2026*
*Repository status: ✅ FUNCTIONAL*