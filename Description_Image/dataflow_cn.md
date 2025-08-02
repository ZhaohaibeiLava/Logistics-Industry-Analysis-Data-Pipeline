---
config:
  theme: redux
---
graph TD
    %% =================================================================
    %% 阶段一：核心数据准备
    %% =================================================================
    subgraph "阶段一：核心数据准备 (数据源 -> 核心中间数据)@zhb"
        A["<b>安监数据</b><br><b style='color:grey'>(输入/安监数据)"] --> B("运行<b style='color:darkblue'>1_data_preprocess.ipynb Cell 2")
        B --> C["<b>拆分后数据<br>（不含顺丰、中通）</b><br><b style='color:grey'>(temp/1_待上传猪猪云文件）"]
        C -- "手动上传" --> D{"猪猪快递云网站"}
        D -- "手动下载" --> E["<b>猪猪云输出数据<br>（不含顺丰、中通）</b><br> <b style='color:grey'>(放入temp/2_猪猪云下载数据"]
        E --> F("运行<b style='color:darkblue'>1_data_preprocess.ipynb Cell 3")
        F --> G["<b>合并数据<br>（不含顺丰、中通）</b><br><b style='color:grey'>（temp/3_猪猪云合并数据）"]

    
        M("运行<b style='color:darkblue'>1_data_preprocess.ipynb Cell 5 中转数据生成")
        G --> M
        M --> N["<b>中转数据<br>（不含顺丰、中通）</b><br><b style='color:grey'>（temp/5_中转数据）"]

        G -- "不含顺丰、中通" --> H{"运行<b style='color:darkblue'>1_data_preprocess.ipynb Cell 4.0-4.8 各公司logistics数据生成"}
        A -- "顺丰、中通" --> H
        H --> I["<b>logistics数据</b><br><b style='color:grey'>（temp/4_logistics数据）"]
        I --> K("运行<b style='color:darkblue'>1_data_preprocess.ipynb Cell 7: 核心数据计算层 <br>")
        N -- "不含顺丰、中通" --> K
        K --> L["<b style='color:darkred'>data_analyisi_result数据</b>"]
        L --> O("运行<b style='color:darkblue'>2_intermediate_DataHub.ipynb Cell 4: 数据中台生成 <br>")
        O --> P["<b style='color:darkred'>分析总报告.xlsx</b>"]
        L --> Q["<b style='color:darkgreen'>邮政月报.xlsx、极兔月报.xlsx</b>"]
        L --> R["<b style='color:darkgreen'>中通月报.xls</b>"]
        P --> R
        L --> S["<b style='color:darkgreen'>1_汇总数据</b>"]
        L --> T["<b style='color:darkgreen'>2_中通报告表格</b>"]
        L --> U["<b style='color:darkgreen'>2_中通报告表格_季度</b>"]
        L --> V["<b style='color:darkgreen'>3_邮政报告表格</b>"]
        L --> W["<b style='color:darkgreen'>4_报告图片</b>"]
        L --> X["<b style='color:darkgreen'>5_通达兔数据</b>"]
        L --> Y["<b style='color:darkgreen'>6_邮政报告表格_季度</b>"]
        L --> Z["<b style='color:darkgreen'>7_报告图片_季度</b>"]
        P --> T["<b style='color:darkgreen'>2_中通报告表格</b>"]
        P --> U["<b style='color:darkgreen'>2_中通报告表格_季度</b>"]
        P --> V["<b style='color:darkgreen'>3_邮政报告表格</b>"]
        P --> W["<b style='color:darkgreen'>4_报告图片</b>"]
        P --> X["<b style='color:darkgreen'>5_通达兔数据</b>"]
        P --> Y["<b style='color:darkgreen'>6_邮政报告表格_季度</b>"]
        P --> Z["<b style='color:darkgreen'>7_报告图片_季度</b>"]

    end

