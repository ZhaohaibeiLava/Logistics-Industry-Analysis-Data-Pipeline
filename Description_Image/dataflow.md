---
config:
  theme: redux
---
graph TD
    %% =================================================================
    %% Stage 1: Core Data Preparation
    %% =================================================================
    subgraph "Stage 1: Core Data Preparation (Raw Sources -> Intermediate Data) @zhb"
        A["<b>Raw Monitoring Data</b><br><b style='color:grey'>(input/monitoring_data)"] --> B("Run <b style='color:darkblue'>1_data_preprocess.ipynb Cell 2")
        B --> C["<b>Split Data<br>(Excludes SF, ZTO)</b><br><b style='color:grey'>(temp/1_to_be_uploaded）"]
        C -- "Manual Upload" --> D{"Cloud Processing Service"}
        D -- "Manual Download" --> E["<b>Processed Cloud Output<br>(Excludes SF, ZTO)</b><br> <b style='color:grey'>(place in temp/2_cloud_download)"]
        E --> F("Run <b style='color:darkblue'>1_data_preprocess.ipynb Cell 3")
        F --> G["<b>Merged Data<br>(Excludes SF, ZTO)</b><br><b style='color:grey'>(temp/3_cloud_merged)"]

    
        M("Run <b style='color:darkblue'>1_data_preprocess.ipynb Cell 5<br>Transit Data Generation")
        G --> M
        M --> N["<b>Transit Data<br>(Excludes SF, ZTO)</b><br><b style='color:grey'>(temp/5_transit_data)"]

        G -- "Excludes SF, ZTO" --> H{"Run <b style='color:darkblue'>1_data_preprocess.ipynb Cell 4.0-4.8<br>Logistics Data Generation"}
        A -- "SF, ZTO only" --> H
        H --> I["<b>Logistics Data</b><br><b style='color:grey'>(temp/4_logistics_data)"]
        
        I --> K("Run <b style='color:darkblue'>1_data_preprocess.ipynb Cell 7<br>Core Data Computation Layer")
        N -- "Excludes SF, ZTO" --> K
        K --> L["<b style='color:darkred'>`data_analysis_result` Outputs</b>"]
        
        L --> O("Run <b style='color:darkblue'>2_intermediate_DataHub.ipynb Cell 4<br>Data Hub Generation")
        O --> P["<b style='color:darkred'>Master_Analysis_Report.xlsx</b>"]
        
        L --> Q["<b style='color:darkgreen'>Postal_Monthly_Report.xlsx, J&T_Monthly_Report.xlsx</b>"]
        L --> R["<b style='color:darkgreen'>ZTO_Monthly_Report.xls</b>"]
        P --> R
        
        L --> S["<b style='color:darkgreen'>1_Summary_Data</b>"]
        L --> T["<b style='color:darkgreen'>2_ZTO_Report_Tables</b>"]
        L --> U["<b style='color:darkgreen'>2_ZTO_Report_Tables_Quarterly</b>"]
        L --> V["<b style='color:darkgreen'>3_Postal_Report_Tables</b>"]
        L --> W["<b style='color:darkgreen'>4_Report_Images</b>"]
        L --> X["<b style='color:darkgreen'>5_Tongda_Series_Data</b>"]
        L --> Y["<b style='color:darkgreen'>6_Postal_Report_Tables_Quarterly</b>"]
        L --> Z["<b style='color:darkgreen'>7_Report_Images_Quarterly</b>"]
        
        P --> T
        P --> U
        P --> V
        P --> W
        P --> X
        P --> Y
        P --> Z
    end