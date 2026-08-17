# Research Artifacts MetaGraph

Research Artifacts MetaGraph is a config-driven web application for browsing and visualizing a coding scheme applied to academic papers. The current instance explores research artifacts coded from Business Process Management (BPM) conference proceedings. The stack consists of React 18, D3.js, and Vite. No backend is required. The output is a static site deployable to any web host or GitHub Pages.

In this case: [Research Artifact MetaGraph Web Application](https://andreamalhera.github.io/nfdixcs_research_artifact_graph-pages/)

## Features

- Types-of-artifact overview that groups papers by artifact type (algorithm, method, framework, model, taxonomy, etc.)
- Scatter-plot research landscape arranged by publication year and track
- Relationship graph with two edge types: shared keywords (IDF-weighted Jaccard) and similar research artifacts (weighted match across coded fields)
- Full-text search across title, authors, and keywords
- Facet filters generated dynamically from the coded fields, plus quick filtering by artifact type
- Side-by-side comparison of two or more papers
- "Add a Paper" flow: extract fields from a DOI (via Crossref), BibTeX, or a plain-text citation, review/edit them, and add the paper locally; visitor-added papers are browser-local only, are visually marked, and can optionally be proposed to the maintainers as a pre-filled GitHub issue on the public mirror
- Dark/light theme toggle with persistence
- Anonymized-paper support: entries can ship with blank title/authors/DOI while still contributing to the landscape and graph, using precomputed keyword-similarity edges so the client never sees the underlying keyword text
- Single JSON config file controlling titles, labels, navigation, coding-scheme categories (types of inquiry, types of artifact), and feature toggles

## Requirements

- Node.js >= 18
- npm (included with Node.js)

## Quick Start

```
git clone <your-repo-url>
cd nfdixcs_research_artifact_graph
npm install
npm run dev
```

The dev server starts at `http://localhost:3000`.


## Data Format

`research_artifacts.json` is a flat array of coded papers, validated against `research_artifacts.schema.json`. Each entry has a `metadata` block (title, authors, DOI/URL, year, track) and a `contribution` block describing keywords, the paper's focus/intent, its research components, and one or more `artifacts`, each carrying its own type(s), research method, evaluation method, data collection, threats to validity, and implementation status.

```json
{
  "metadata": {
    "title": "Paper Title",
    "authors": ["Author A", "Author B"],
    "doi_or_url": "https://doi.org/...",
    "year": 2025,
    "track": "Engineering"
  },
  "contribution": {
    "keywords": ["process mining", "conformance checking"],
    "focus_intent": {
      "goal_paper": "...",
      "type_of_inquiry": ["information_systems_engineering"]
    },
    "research_components": {
      "emphasis": ["artifact"]
    },
    "artifacts": [
      {
        "type_of_artifact": ["method"],
        "research_method": { "methods": ["design_science_engineering"] },
        "evaluation_method": ["case_study"],
        "data_collection": { "data_type": ["real_world_data"] },
        "threats_to_validity": ["external_validity"],
        "implementation": { "existence": true, "availability": true }
      }
    ]
  }
}
```

## Building for Production

The `build` command generates a static site in `dist/`.

```
npm run build
```

The `dist/` folder can be served by any static file server.

### GitHub Pages

The base path must be set via environment variable before building.

```
BASE_URL=/your-repo-name/ npm run build
```

## Development

The following commands are available during development.

```
npm run dev       # Start dev server with hot reload
npm run build     # Production build
npm run preview   # Preview production build locally
```
## Acknowledgements

We thank Christian Imenkamp for his input in usibility and design, which greatly improved this web application.

## License

The dataset and site content are licensed under CC BY 4.0 (see the About page in the running application for the full notice).

### Citation
The `Research Artifacts MetaGraph` is part of an [NFDIxCS Service](https://nfdixcs.org/services). For extensions, please submit a pull request or contact the author, [Andrea Maldonado](mailto:andreamalher.works@gmail.com).

```bibtex
@InProceedings{maldonado2026metagraph,
author="Maldonado, Andrea
and Koschmider, Agnes
title="Research Artifacts MetaGraph: A Tool for Comparing and Contextualizing Scientific Contributions in Computer Science",
year="2026",
publisher="Zenodo",
doi = {10.5281/zenodo.21946693},
url = {https://doi.org/10.5281/zenodo.21946693}
}
```

### Acknoledgements:
Funded by the German Research Foundation (DFG) within the framework of NFDIxCS (DFG project number 501930651).
