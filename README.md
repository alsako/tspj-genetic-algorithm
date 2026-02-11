
# Genetic Algorithm for TSPJ (Notebook)

This repository contains a Jupyter notebook (`ga_tspj.ipynb`) implementing a Genetic Algorithm for a TSPJ-style problem where a solution consists of:

1.  a permutation of stations (including station 0 as the depot/start),
    
2.  a permutation/order of jobs.
    

The objective (fitness) is computed as the maximum completion time among all executed jobs, based on:

-   d(i, j): travel time between stations
    
-   t(i, j): processing time for job j at station i
    

The notebook reads an instance file, runs the GA, and plots:

-   best solution cost per generation
    
-   average population cost per generation
    

## Algorithm details (as implemented)

-   Chromosome: (station tour, job order)
    
-   Initialization: random station tour (station 0 fixed at start) + random job order
    
-   Selection: rank-based roulette selection (implemented in `rulet`)
    
-   Crossover: Order Crossover (OX) applied separately to:
    
    -   station tour (excluding station 0, then reinserted)
        
    -   job order
        
-   Mutation: swap mutation (independently applied to tour and jobs) with mutation rate 0.2
    
-   Replacement: periodic immigrant injection is implemented (function `imigranti`) and can be enabled in the GA loop
    
-   Population size: 20
    
-   Generations: 10000
    
-   Runs: the notebook runs the GA 3 times and prints the average result
    

## Files

-   ga_tspj.ipynb — main notebook
    
-   requirements.txt — Python dependencies for local execution
    
-   .gitignore — ignores environments, caches, and optional instance/data folders
    

## How to run

Option A: Google Colab (recommended)

1.  Upload `ga_tspj.ipynb` to Colab and open it.
    
2.  Run the cells.
    
3.  When prompted, upload the instance text file using the file upload dialog (the notebook uses `google.colab.files.upload()`).
    

Option B: Run locally (Jupyter)  
The notebook is written with Colab upload logic. To run locally:

1.  Create and activate a virtual environment.  
    Windows:  
    python -m venv .venv  
    .venv\Scripts\activate
    

macOS/Linux:  
python3 -m venv .venv  
source .venv/bin/activate

2.  Install dependencies:  
    pip install -r requirements.txt
    
3.  Open Jupyter:  
    jupyter notebook
    
4.  Open ga_tspj.ipynb.
    
5.  Replace the Colab upload section:
    

-   Remove or comment out:  
    from google.colab import files  
    uploaded = files.upload()  
    filename = list(uploaded.keys())[0]
    
-   Replace with a local filename, for example:  
    filename = "instance.txt"
    

Then run the notebook cells normally.

## Input format (instance file)

The notebook expects a text file formatted as:

-   first line: integer n (number of jobs)
    
-   next (n + 1) lines: (n + 1) integers per line for distance matrix d
    
-   next n lines: n integers per line for processing matrix t

