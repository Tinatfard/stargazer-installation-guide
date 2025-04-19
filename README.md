# Stargazer v2.0.3 Installation Guide

This repository provides a comprehensive guide to install [**Stargazer**](https://stargazer.gs.washington.edu/stargazerweb/res/documentation.html), a computational tool for calling star alleles from next-generation sequencing (NGS) data. The guide focuses on installation under **Ubuntu 22.04** or **Windows Subsystem for Linux (WSL)** using **Python 3.8.2**, including required dependencies and fixes for `ModuleNotFoundError`.

---

## 📑 Table of Contents

- [📋 Prerequisites](#-prerequisites)
- [⚙️ Installation Steps](#-installation-steps)
- [🛠️ Modifications](#️-modifications)
- [🧹 Remaining Tasks](#-remaining-tasks)
- [✅ Verification](#-verification)
- [📚 Additional Resources](#-additional-resources)
- [📄 License](#-license)
- [🙏 Acknowledgments](#-acknowledgments)

---

## 📋 Prerequisites

### System
- **Operating System**: Ubuntu 22.04 or WSL (Windows 10/11)
- **Python**: 3.8.2
- **Java**: OpenJDK 11 (e.g., 11.0.26)

### System Dependencies
```bash
build-essential
python3-dev
libbz2-dev
liblzma-dev
libcurl4-openssl-dev
libssl-dev
zlib1g-dev
```

### Python Dependencies (exact versions)
```bash
pysam==0.23.0
numpy==1.24.4
pandas==2.0.3
scipy==1.10.1
matplotlib==3.7.5
```

---

## ⚙️ Installation Steps

### 1️⃣ Install System Dependencies
```bash
sudo apt update
sudo apt install -y python3-pip python3-venv build-essential python3-dev \
libbz2-dev liblzma-dev libcurl4-openssl-dev libssl-dev zlib1g-dev \
git openjdk-11-jdk
```

### 2️⃣ Set Up Virtual Environment
```bash
mkdir stargazer_project
cd stargazer_project
python3 -m venv pysam_env
source pysam_env/bin/activate
```

### 3️⃣ Install Python Dependencies
```bash
python -m pip install --upgrade pip setuptools wheel
pip install pysam==0.23.0 numpy==1.24.4 pandas==2.0.3 scipy==1.10.1 matplotlib==3.7.5
```

### 4️⃣ Download and Extract Stargazer

Download Stargazer v2.0.3 from the [official site](https://stargazer.gs.washington.edu/stargazerweb/res/form.html) and extract it:

```bash
unzip Stargazer_v2.0.3.zip -d Stargazer_v2.0.3
cd Stargazer_v2.0.3
chmod -R u+rw .
```

### 5️⃣ Apply Modifications  
(See [Modifications](#️-modifications) section.)

### 6️⃣ Install Stargazer
```bash
python setup.py install
```

### 7️⃣ Verify Installation
```bash
python -m stargazer --help
```

---

## 🛠️ Modifications

To resolve `ModuleNotFoundError`, apply the following changes:

<details>
<summary><code>stargazer/phenotyper.py</code></summary>

```diff
- from common import get_stardb
+ from .common import get_stardb
```
</details>

<details>
<summary><code>stargazer/common.py</code></summary>

```diff
- from sglib import sort_regions
+ from .sglib import sort_regions
```
</details>

<details>
<summary><code>stargazer/bam2gdf.py</code></summary>

```diff
- from bam2sdf import bam2sdf
+ from .bam2sdf import bam2sdf
```
</details>

<details>
<summary><code>stargazer/bam2sdf.py</code></summary>

```diff
- from common import ...
+ from .common import ...
- from sglib import ...
+ from .sglib import ...
```
</details>

<details>
<summary><code>stargazer/__main__.py</code></summary>

```diff
- from phenotyper import _phenotype_default
+ from .phenotyper import _phenotype_default
- from bam2gdf import bam2gdf
+ from .bam2gdf import bam2gdf
```
</details>

---

## 🧹 Remaining Tasks

### 🔧 Syntax Warnings in `__main__.py`
```diff
- gt = [int(y) if y is not "." else y for y in gt]
+ gt = [int(y) if y != "." else y for y in gt]

- ad_list = [int(y) if y is not "." else 0 for y in ad_list]
+ ad_list = [int(y) if y != "." else 0 for y in ad_list]
```

### 🔧 Fix SyntaxError in `check_impute_calls.py`
```diff
- if "0|0" in gt_phased:
-     next
+ if "0|0" in gt_phased:
+     continue
```

---

## ✅ Verification

Ensure all modules are accessible:

```bash
source pysam_env/bin/activate
python -c "import stargazer.phenotyper; print(dir(stargazer.phenotyper))"
python -c "import stargazer.common; print(dir(stargazer.common))"
python -c "import stargazer.sglib; print(dir(stargazer.sglib))"
python -c "import stargazer.bam2sdf; print(dir(stargazer.bam2sdf))"
python -c "import stargazer.bam2gdf; print(dir(stargazer.bam2gdf))"
python -c "import stargazer.sdf2gdf; print(dir(stargazer.sdf2gdf))"
python -c "import stargazer.check_impute_calls; print(dir(stargazer.check_impute_calls))"
python -c "import stargazer.version; print(dir(stargazer.version))"
```

---

## 📚 Additional Resources

- [pysam Documentation](https://pysam.readthedocs.io/en/latest/)
- [WSL Docs](https://learn.microsoft.com/en-us/windows/wsl/)
- [Python 3.8.2 Documentation](https://docs.python.org/3.8/)

---

## 📄 License

This guide and all modification instructions are provided for educational and reproducibility purposes.  
> ⚠️ **Note:** Stargazer itself is not open-source. Please obtain it only from the [official website](https://stargazer.gs.washington.edu/stargazerweb/res/form.html). Do not redistribute its source code.

---

## 🙏 Acknowledgments

- [Stargazer Project – sbstevenlee/Stargazer](https://github.com/sbstevenlee/Stargazer)
- University of Washington
- The bioinformatics and Python open-source community

---