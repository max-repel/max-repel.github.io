# Dowsing Machine

# Data Flow and Structure

```mermaid
graph TD
    subgraph "Data Sources"
        A[PokeAPI - REST]
        B[Smogon Monthly Stats - JSON]
    end

    subgraph "Processing (Python)"
        C{Data Extraction}
        D[Normalize: ID, Moves, Abilities]
        E[Map Smogon Stats to PokeAPI IDs]
    end

    subgraph "Storage (Parquet/OLAP)"
        F[(Raw Parquet Files: ability.parquet, moves.parquet)]
        G[(Enriched Parquet: smogon_moves.parquet, etc.)]
        H[DuckDB Views]
    end

    subgraph "Analytics"
        I[Apache Superset Dashboards]
    end

    A --> C
    B --> E
    C --> D
    D --> F
    F --> E
    E --> G
    G --> H
    H --> I
    F -.->|Optional| H
    
   
