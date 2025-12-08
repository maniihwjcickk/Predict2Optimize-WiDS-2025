# Week 1 — Intro to Data Science in Python through Financial Data and Feature Extraction

In Week 1, you will set up your environment, download real financial data, and do basic processing to understand what later weeks will build on.  
All tasks are completed inside the provided **Jupyter Notebook(s)**, which include partially filled code and instructions.  
After setup, look at **README.ipynb** for an intro to the libraries and concepts used this week.

**Deadline: 13 Dec 2025**

---

## **1. Setup Instructions**

> [!note] If you're new to Python or Git  
> You only need the basics to follow this project. Beginner-friendly resources are listed at the bottom.  
> Ask questions on the group if you're stuck with setup.

---

### **1.1 Get the source code**
> [!note] TLDR: Fork the repo. Work in your fork. At each deadline, create a branch `submission-week{i}` so we have a fixed snapshot to check.

1. **Fork** this repository to your own GitHub account.  
2. **Clone** your fork locally and work directly in it.
3. Commit and push changes normally (to your `main`):

```bash
git add .
git commit -m "Describe changes"
git push
```

4. **At each submission deadline**, create a branch for that week's submission:

```bash
git checkout -b submission-week2   # example for Week 2
git push -u origin submission-week2
```

Submit **the link to this branch**.  
This branch acts as a fixed snapshot — later changes will not affect your submission.

5. **(Optional)** To sync with the original repo:

```bash
git remote add upstream https://github.com/sushantpadha/Predict2Optimize-WiDS-2025
git fetch upstream
git merge upstream/main
```

---

### **1.2 Create and activate a virtual environment**

```bash
python3 -m venv .venv
source .venv/bin/activate        # Linux/Mac
# OR
.\.venv\Scripts\Activate.ps1     # Windows PowerShell
```

---

### **1.3 Install project dependencies**

```bash
pip install numpy pandas matplotlib yfinance scikit-learn seaborn scipy statsmodels
pip install ipykernel
```

---

## **2. Recommended Editor: VS Code + Jupyter**

1. Install VS Code  
2. Install the **Python** and **Jupyter** extensions  
3. Open this project folder  
4. Select the virtual environment (`.venv`)  
5. Open the notebooks provided in the repo  

---

## **3. Financial Data Basics (Covered in the Notebook)**

You will work with:

* Adjusted Close prices from `yfinance`
* Simple and log returns
* Rolling-window features:
  * 5-day returns  
  * 20-day volatility  
  * 10-day momentum  

The notebook walks you through:

* downloading data
* cleaning missing values
* computing returns
* generating rolling features
* plotting price and return series

---

## **4. Week 1 Tasks**

All tasks are mentioned in the notebook.

---

## **5. Resources**

For detailed info on any of the libraries please refer to official documentation.

*Cheatsheets*
* Pandas - https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf  
* Rolling — https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rolling.html 
* Matplotlib - https://matplotlib.org/cheatsheets/cheatsheets.pdf
* Seaborn - https://github.com/jramshur/Coding-Cheat-Sheets/blob/master/Python%20for%20Data%20Science%20-%20Cheat%20Sheet%20-%20Seaborn.pdf
* Scipy - https://github.com/jramshur/Coding-Cheat-Sheets/blob/master/Python%20for%20Data%20Science%20-%20Cheat%20Sheet%20-%20SciPy%20-%20Lineary%20Algebra.pdf

*yfinance*
* yfinance quickstart — https://ranaroussi.github.io/yfinance/
* yfinance more info - https://algotrading101.com/learn/yfinance-guide/
* Why log returns — https://quantivity.wordpress.com/2011/02/21/why-log-returns/

The portfolio optimization book (in project README) is referred to as well, specifically chapters 1, 2.

---

## **7. Week 1 Deliverables**

Submit your notebook branch (`submission-week1`) containing week 1 notebooks with finished code.
