
# Semantic Web with RDFlib: Bahria University Courses Example

This repository contains a Google Colab notebook demonstrating the use of RDFlib for Semantic Web data manipulation, specifically focusing on representing and querying course information from Bahria University.

## Project Overview

The project uses [RDFlib](https://rdflib.readthedocs.io/en/stable/) to:
- Define a knowledge graph using Turtle syntax.
- Load and parse RDF data.
- Execute SPARQL queries to retrieve specific information from the graph.

## Data Model

The data is modeled using common RDF prefixes:
- `foaf`: Friend of a Friend (for person details like name and email)
- `schema`: Schema.org (for courses, course names, codes, descriptions, and providers)
- `rdf`: RDF Schema (for defining types)

### Example Turtle Data:

```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix schema: <http://schema.org/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<#CSC401>
  a schema:Course ;
  schema:name "Knowledge Representation & Reasoning" ;
  schema:courseCode "CSC-401" ;
  schema:description "Study of logic-based methods for knowledge modeling, RDF, and SPARQL." ;
  schema:provider [
    a schema:Person ;
    foaf:name "Dr. M. Ali Khan" ;
    foaf:mbox <mailto:ali.khan@bahria.edu.pk> ;
    foaf:title "Associate Professor"
  ] .

<#CSC505>
  a schema:Course ;
  schema:name "Game Development & AI" ;
  schema:courseCode "CSC-505" ;
  schema:description "Advanced Unity development involving ML-Agents and 3D physics." ;
  schema:provider [
    a schema:Person ;
    foaf:name "Ms. Sana Ahmed" ;
    foaf:mbox <mailto:sana.ahmed@bahria.edu.pk>
  ] .
```

## Queries

The notebook demonstrates two types of SPARQL queries:

1.  **List Courses:** Retrieves the name and code of all courses defined in the graph.
    ```sparql
    PREFIX schema: <http://schema.org/>
    SELECT ?courseName ?code
    WHERE {
      ?course a schema:Course ;
              schema:name ?courseName ;
              schema:courseCode ?code .
    }
    ```

2.  **Find Instructor:** Finds the instructor and their email for a specific course (e.g., "Knowledge Representation & Reasoning").
    ```sparql
    PREFIX schema: <http://schema.org/>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    SELECT ?instructorName ?email
    WHERE {
      ?course schema:name "Knowledge Representation & Reasoning" ;
              schema:provider ?teacher .
      ?teacher foaf:name ?instructorName ;
               foaf:mbox ?email .
    }
    ```

## Setup and Usage (Google Colab)

1.  **Open the Notebook:** Upload or open the `.ipynb` file in Google Colab.
2.  **Install Dependencies:** The first cell installs `rdflib`.
    ```python
    !pip install rdflib
    ```
3.  **Run Cells:** Execute the cells sequentially to load the data and run the SPARQL queries.

## Requirements

- Python 3.x
- `rdflib` library (`pip install rdflib`)

## Output Example

```
--- RESULTS: QUERY 1 (COURSES) ---
Course: Knowledge Representation & Reasoning, Code: CSC-401
Course: Game Development & AI, Code: CSC-505

--- RESULTS: QUERY 2 (INSTRUCTOR) ---
Instructor: Dr. M. Ali Khan, Email: mailto:ali.khan@bahria.edu.pk
```

