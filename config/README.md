# 🔧 Configuration Setup

To use this systematic review dataset repository, you need to configure API keys and credentials.

## 📋 Required Files

Create these files in the `config/` directory:

### 1. `cochrane_cookie.txt`
- Get cookie from Cochrane Library website
- Required for accessing Cochrane systematic reviews

### 2. `core_api_key.txt`
- Get API key from: https://core.ac.uk/services/api
- Required for downloading PDFs from CORE database

### 3. `semanticscholar_api_key.txt`
- Get API key from: https://www.semanticscholar.org/product/api
- Required for downloading PDFs from Semantic Scholar

### 4. `entrez_email.txt`
- Your email address for PubMed Entrez API
- Required for accessing PubMed data

### 5. `grobid_config.json`
- Copy from `grobid_config.template.json`
- Update `grobid_server` URL with your GROBID server
- For GROBID setup: https://grobid.readthedocs.io/en/latest/Install-Grobid/

## 🚀 Quick Setup

```bash
# Copy template
cp grobid_config.template.json grobid_config.json

# Edit with your server URL
# Then add your API keys to the other files
```

## ⚠️ Security

**NEVER commit these files to git!** They contain sensitive credentials.

The `.gitignore` file already excludes them for your safety.