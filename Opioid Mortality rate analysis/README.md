{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "# Stage I - Data Understanding and Linking\n",
    "\n",
    "## What is the U.S. Opioid Epidemic?\n",
    "\n",
    "- In the late 1990s, pharmaceutical companies reassured the medical community that patients would not become addicted to opioid pain relievers and healthcare providers began to prescribe them at greater rates.\n",
    "\n",
    "- Increased prescription of opioid medications led to widespread misuse of both prescription and non-prescription opioids before it became clear that these medications could indeed be highly addictive.\n",
    "\n",
    "![opioid](https://www.hhs.gov/opioids/sites/default/files/inline-images/opioids-infographic.png)\n",
    "\n",
    "Source: https://www.hhs.gov/opioids/about-the-epidemic/index.html\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We are going to study the underlying patterns that exist between opioid related deaths and the different socio-economic, demographic, geographic, and equity related variables that are available for US population. Our goal is to extract such patterns and understand them futher using data science techniques. \n",
    "\n",
    "In order to achieve that, the project is separated into 5 stages:\n",
    "\n",
    "- Stage I - Data and Project Understanding,\n",
    "- Stage II - Data Modeling,\n",
    "- Stage III - Distributions and Hypothesis Testing,\n",
    "- Stage IV - Dashboard\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "\n",
    "### Opioid overdose dataset linking\n",
    "\n",
    "In this stage we utilize multiple publicly available datasets and link them together for analytics. Our goal here is to help identify patterns which contribute to drug overdose deaths. Within this notebook we will explore:\n",
    "\n",
    "1. **Creating Index** - Developing an index key for linking datasets\n",
    "2. **Join** - Using join to merge data based on index key.\n",
    "\n",
    "The notebooks is viewable via any browser. \n",
    "\n",
    "#### Software used (open source):\n",
    "\n",
    "- `python` - https://www.python.org/download/releases/3.0/\n",
    "- `pandas` - https://pandas.pydata.org/\n",
    "- `plotly` - https://plotly.com/"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "### Datasets\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "source": [
    "#### 1. Drug Overdose Dataset\n",
    "\n",
    "The overdose death/cause dataset was obtained from CDC Wonder (https://wonder.cdc.gov/ucd-icd10.html). The dataset is from the Underlying Cause of Death database contains mortality and population counts for all U.S. counties. Data are based on death certificates for U.S. residents. Each death certificate identifies a single underlying cause of death and demographic data. \n",
    "\n",
    "- From this data we obtained the Drug/Alcohol Induced causes data for 2019 across all counties in US. \n",
    "- https://wonder.cdc.gov/wonder/help/ucd.html#Drug/Alcohol%20Induced%20Causes\n",
    "- File: `./data/Underlying Cause of Death-County-2019.txt`"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "#### 2. County Health Rankings\n",
    "\n",
    "The County Health Rankings provide a snapshot of a community’s health and a starting point for investigating and discussing ways to improve health. The annual Rankings measures vital health factors, including high school graduation rates, obesity, smoking, unemployment, access to healthy foods, the quality of air and water, income inequality, and teen births in nearly every county in America. The dataset provides a snapshot of how health is influenced by where we live, learn, work and play.\n",
    "\n",
    "- From this data we obtained the measures data for 2019 across all counties in US. \n",
    "- https://www.countyhealthrankings.org/\n",
    "- Data Dictionary - https://www.countyhealthrankings.org/sites/default/files/DataDictionary_2019.pdf\n",
    "- File: `./data/County_Health_Ranking.csv`"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "#### 3. County Opioid Dispensing Rates\n",
    "\n",
    "The third dataset in this notebook is the Opoid Dispensing Rate dataset. The dataset has geographic distribution of retail opioid prescriptions dispensed per 100 persons per year from 2006–2019. Rates are classified by the Jenks natural breaks classification method into four groups using the 14-year range of data to determine the class breaks. \n",
    "\n",
    "- We utilize County Opoid Dispensing Rates for 2019.\n",
    "- https://www.cdc.gov/drugoverdose/maps/rxcounty2019.html\n",
    "- File: `./data/2019-Opioid_Rate.csv`"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   }
   