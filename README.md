flowchart LR

subgraph S[🌐 External Data Sources]
  G[Google]
  Y[Yahoo!]
  F[Facebook]
  X[Twitter / X]
end

subgraph D[🔁 Databeat]
  DB[Databeat\n(Data Collection / Integration)]
end

subgraph C[☁️ Google Cloud Project]
  GCS[(Cloud Storage)]
  DS[(Cloud Datastore)]
  BQ[(BigQuery)]
end

subgraph R[📊 Reporting / BI]
  LS[Looker Studio]
  TB[Tableau]
  XL[Excel Report]
end

%% ---- Data collection ----
G -->|Data collection| DB
Y -->|Data collection| DB
F -->|Data collection| DB
X -->|Data collection| DB

%% ---- Data write to GCP ----
DB -->|Data write| GCS
DB -->|Data write| DS
DB -->|Data write| BQ

%% ---- BI / reporting ----
BQ -->|Query / visualization| LS
BQ -->|Extract / connect| TB

%% ---- Excel generation flow ----
GCS -->|Data read (for report)| DB
BQ -->|Data read (for report)| DB
DB -->|Export| XL
