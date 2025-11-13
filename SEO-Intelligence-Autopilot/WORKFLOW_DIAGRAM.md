# 📊 SEO Intelligence Autopilot - Workflow Diagrams

## 🎯 Overview: High-Level Flow

```mermaid
graph TB
    Start([🌐 User Input: URL]) --> Input[📥 INPUT PHASE]
    Input --> Discovery[🔍 DISCOVERY PHASE]
    Discovery --> SERP[🎭 SERP INTELLIGENCE]
    SERP --> Gap[💎 GAP ANALYSIS]
    Gap --> AI[🧠 AI STRATEGY]
    AI --> Output[📤 OUTPUT PHASE]
    Output --> End([✅ Complete!])

    style Start fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    style Input fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style Discovery fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style SERP fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style Gap fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    style AI fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style Output fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    style End fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px
```

---

## 🔄 Detailed Node-Level Flow

```mermaid
graph TB
    subgraph INPUT["📥 INPUT PHASE"]
        A[Webhook: URL Input]
        B[Respond: Started]
        C[Extract Domain]
    end

    subgraph DISCOVERY["🔍 DISCOVERY PHASE"]
        D[DataForSEO:<br/>Keywords For Site]
        E[Process Keywords]
        F[Split Top 5]
    end

    subgraph SERP["🎭 SERP INTELLIGENCE"]
        G[DataForSEO:<br/>SERP Analysis]
        H[Analyze Competitors<br/>& SERP Features]
        I[Merge Initial Data]
    end

    subgraph GAPS["💎 GAP ANALYSIS"]
        J[DataForSEO:<br/>Competitor Keywords]
        K[Process<br/>Competitor Data]
        L[Merge All Data]
    end

    subgraph AI["🧠 AI STRATEGY"]
        M[Prepare<br/>Claude Prompt]
        N[Claude Sonnet-4.5:<br/>Strategic Analysis]
    end

    subgraph OUTPUT["📤 OUTPUT PHASE"]
        O[Google Docs:<br/>Create Report]
        P[Google Sheets:<br/>Update Tracker]
        Q[Slack:<br/>Notification]
    end

    A --> B
    A --> C
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I --> J
    I --> L
    J --> K
    K --> L
    L --> M
    M --> N
    N --> O
    N --> P
    O --> Q
    P --> Q

    style INPUT fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style DISCOVERY fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style SERP fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style GAPS fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    style AI fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style OUTPUT fill:#fff9c4,stroke:#f57f17,stroke-width:2px
```

---

## 📊 Data Flow Diagram

```mermaid
graph LR
    subgraph INPUT_DATA["INPUT DATA"]
        URL[🌐 Website URL<br/>hyroxtrainingplans.com]
    end

    subgraph EXTRACTED["EXTRACTED DATA"]
        DOM[Domain: hyroxtrainingplans.com]
    end

    subgraph KEYWORD_DATA["KEYWORD DISCOVERY"]
        KW[50 Keywords Found:<br/>• hyrox training<br/>• hyrox workouts<br/>• Position: 3-15<br/>• Volume: 100-5000]
    end

    subgraph SERP_DATA["SERP ANALYSIS"]
        TOP5[Top 5 Keywords<br/>analyzed in SERP]
        COMP[Competitors Found:<br/>• competitor1.com<br/>• competitor2.com<br/>• competitor3.com]
        FEAT[SERP Features:<br/>• Featured Snippets<br/>• People Also Ask<br/>• Related Searches]
    end

    subgraph GAP_DATA["GAP ANALYSIS"]
        CGAP[Competitor Keywords:<br/>30 keywords they rank for]
        GAPS[Keyword Gaps Found:<br/>15 opportunities<br/>we don't rank for]
    end

    subgraph AI_DATA["AI PROCESSING"]
        PROMPT[Comprehensive Prompt<br/>with all data]
        STRAT[Strategic Analysis:<br/>• Opportunities<br/>• Content Ideas<br/>• Action Plan]
    end

    subgraph OUTPUT_DATA["OUTPUT"]
        DOC[📄 Google Doc:<br/>SEO Strategy Report]
        SHEET[📊 Google Sheet:<br/>Keyword Tracker]
        NOTIF[📧 Slack Notification]
    end

    URL --> DOM
    DOM --> KW
    KW --> TOP5
    TOP5 --> COMP
    TOP5 --> FEAT
    COMP --> CGAP
    CGAP --> GAPS
    KW --> PROMPT
    COMP --> PROMPT
    GAPS --> PROMPT
    FEAT --> PROMPT
    PROMPT --> STRAT
    STRAT --> DOC
    STRAT --> SHEET
    DOC --> NOTIF
    SHEET --> NOTIF

    style INPUT_DATA fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style EXTRACTED fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style KEYWORD_DATA fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style SERP_DATA fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style GAP_DATA fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    style AI_DATA fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style OUTPUT_DATA fill:#fff9c4,stroke:#f57f17,stroke-width:2px
```

---

## 🔀 Parallel Processing Flow

```mermaid
graph TB
    START[Process Keywords Data]

    START --> SPLIT[Split Top 5 Keywords]

    SPLIT --> S1[SERP: Keyword 1]
    SPLIT --> S2[SERP: Keyword 2]
    SPLIT --> S3[SERP: Keyword 3]
    SPLIT --> S4[SERP: Keyword 4]
    SPLIT --> S5[SERP: Keyword 5]

    S1 --> AGG[Analyze & Aggregate<br/>Competitor Data]
    S2 --> AGG
    S3 --> AGG
    S4 --> AGG
    S5 --> AGG

    AGG --> C1[Get Competitor 1<br/>Keywords]
    AGG --> C2[Get Competitor 2<br/>Keywords]
    AGG --> C3[Get Competitor 3<br/>Keywords]

    C1 --> MERGE[Merge All Data]
    C2 --> MERGE
    C3 --> MERGE
    START --> MERGE

    MERGE --> AI[Claude Analysis]

    AI --> OUT1[Google Docs]
    AI --> OUT2[Google Sheets]

    OUT1 --> NOTIFY[Slack Notification]
    OUT2 --> NOTIFY

    style START fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style SPLIT fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style AGG fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style MERGE fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style AI fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style NOTIFY fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

---

## 🎯 API Integration Flow

```mermaid
graph TB
    subgraph USER["👤 USER"]
        INPUT[Submit URL]
    end

    subgraph N8N["⚙️ N8N WORKFLOW"]
        WH[Webhook Receiver]
        PROC[Data Processing<br/>& Orchestration]
    end

    subgraph DATAFORSEO["📊 DATAFORSEO API"]
        API1[Keywords For Site<br/>GET ranking keywords]
        API2[SERP API<br/>GET search results]
        API3[Competitor Keywords<br/>GET competitor data]
    end

    subgraph CLAUDE["🤖 ANTHROPIC CLAUDE"]
        AI[Sonnet-4.5<br/>Strategic Analysis]
    end

    subgraph GOOGLE["📁 GOOGLE WORKSPACE"]
        DOCS[Google Docs API<br/>Create Report]
        SHEETS[Google Sheets API<br/>Update Tracker]
    end

    subgraph SLACK["💬 SLACK"]
        NOTIFY[Send Notification]
    end

    INPUT --> WH
    WH --> PROC

    PROC -->|1. Discover Keywords| API1
    API1 -->|50 Keywords| PROC

    PROC -->|2. Analyze SERP| API2
    API2 -->|Top 10 Results| PROC

    PROC -->|3. Get Competitor Data| API3
    API3 -->|30 Keywords| PROC

    PROC -->|4. Generate Strategy| AI
    AI -->|Markdown Report| PROC

    PROC -->|5. Create Document| DOCS
    DOCS -->|Doc URL| PROC

    PROC -->|6. Update Spreadsheet| SHEETS
    SHEETS -->|Sheet URL| PROC

    PROC -->|7. Alert User| NOTIFY

    style USER fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    style N8N fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style DATAFORSEO fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style CLAUDE fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style GOOGLE fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style SLACK fill:#fce4ec,stroke:#880e4f,stroke-width:2px
```

---

## 🔄 Decision Flow: Competitor Discovery Logic

```mermaid
graph TD
    START[SERP Data<br/>from Top 5 Keywords]

    START --> EXTRACT[Extract All Domains<br/>from Top 10 Results]

    EXTRACT --> FILTER{Filter Domain}

    FILTER -->|Own Domain| SKIP[Skip]
    FILTER -->|Generic Site| SKIP2[Skip:<br/>Wikipedia, Amazon, etc.]
    FILTER -->|Valid Competitor| COUNT[Count Appearances]

    COUNT --> RANK[Rank by Frequency]

    RANK --> TOP3{Top 3<br/>Competitors?}

    TOP3 -->|Yes| ANALYZE[Analyze Each<br/>Competitor]
    TOP3 -->|No| DONE1[Use Available Data]

    ANALYZE --> KWDATA[Get Keywords<br/>For Site]

    KWDATA --> GAPS[Calculate<br/>Keyword Gaps]

    GAPS --> PRIORITY[Prioritize by<br/>Opportunity Score]

    PRIORITY --> OUTPUT[Output to<br/>Claude Analysis]
    DONE1 --> OUTPUT

    style START fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style FILTER fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style TOP3 fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    style OUTPUT fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

---

## 📈 Example: Real Execution Flow for hyroxtrainingplans.com

```mermaid
graph TB
    subgraph INPUT["INPUT"]
        URL["URL:<br/>hyroxtrainingplans.com"]
    end

    subgraph DISCOVERY["KEYWORD DISCOVERY"]
        KW1["Found 47 Keywords:<br/>• hyrox training (2400 vol)<br/>• hyrox workouts (880 vol)<br/>• hyrox preparation (320 vol)<br/>• ...<br/>Avg Position: 8.3"]
    end

    subgraph SERP["SERP ANALYSIS - TOP 5"]
        S1["hyrox training<br/>→ Top 10 domains"]
        S2["hyrox workouts<br/>→ Top 10 domains"]
        S3["hyrox preparation<br/>→ Top 10 domains"]
        S4["hyrox exercises<br/>→ Top 10 domains"]
        S5["hyrox tips<br/>→ Top 10 domains"]
    end

    subgraph COMPETITORS["COMPETITORS FOUND"]
        C1["1. trainingpeaks.com<br/>(appeared 4x)"]
        C2["2. wodprep.com<br/>(appeared 3x)"]
        C3["3. barbend.com<br/>(appeared 3x)"]
    end

    subgraph GAPS["KEYWORD GAPS"]
        G1["'hyrox training plan pdf'<br/>Vol: 1200, Their Pos: 3"]
        G2["'hyrox nutrition guide'<br/>Vol: 480, Their Pos: 5"]
        G3["'hyrox beginner tips'<br/>Vol: 320, Their Pos: 7"]
    end

    subgraph AI["AI ANALYSIS"]
        PROMPT["Claude Prompt:<br/>• Current: 47 keywords<br/>• Competitors: 3 domains<br/>• Gaps: 15 opportunities<br/>• SERP: Featured Snippets<br/>• PAA: 8 questions"]
        RESULT["Strategy Generated:<br/>• Quick Win: Target PDF guide<br/>• Content: Nutrition article<br/>• SEO: Optimize for snippets<br/>• Priority: 10 action items"]
    end

    subgraph OUTPUT["OUTPUT"]
        DOC["Google Doc:<br/>'SEO Strategy - hyroxtrainingplans.com'<br/>• 8-page report<br/>• 10 opportunities<br/>• 5 content ideas<br/>• Action checklist"]
        SHEET["Google Sheet:<br/>• 47 current keywords<br/>• 15 opportunities<br/>• 3 competitor profiles<br/>• Tracking setup"]
    end

    URL --> KW1
    KW1 --> S1 & S2 & S3 & S4 & S5
    S1 & S2 & S3 & S4 & S5 --> C1 & C2 & C3
    C1 & C2 & C3 --> G1 & G2 & G3
    KW1 & G1 & G2 & G3 --> PROMPT
    PROMPT --> RESULT
    RESULT --> DOC & SHEET

    style INPUT fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style DISCOVERY fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style SERP fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style COMPETITORS fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style GAPS fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    style AI fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style OUTPUT fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

---

## ⏱️ Timing Diagram

```mermaid
gantt
    title SEO Intelligence Autopilot - Execution Timeline
    dateFormat  ss
    axisFormat %S sec

    section Input
    Webhook Receive           :done, 00, 1s
    Extract Domain            :done, 01, 1s

    section Discovery
    Keywords For Site API     :active, 02, 8s
    Process Keywords          :active, 10, 2s
    Split Top 5               :active, 12, 1s

    section SERP
    SERP Analysis (5 calls)   :crit, 13, 15s
    Analyze Competitors       :crit, 28, 3s

    section Gaps
    Competitor Keywords (3x)  :31, 12s
    Process Gap Data          :43, 2s
    Merge All                 :45, 1s

    section AI
    Prepare Prompt            :46, 1s
    Claude Analysis           :crit, 47, 25s

    section Output
    Create Google Doc         :72, 5s
    Update Google Sheet       :72, 3s
    Send Notification         :77, 2s

    section Complete
    Done                      :milestone, 79, 0s
```

**Total Time: ~80 seconds (1:20 minutes)**

---

## 🔀 Error Handling Flow (Future Enhancement)

```mermaid
graph TB
    START[Node Execution]

    START --> EXEC{Execute API Call}

    EXEC -->|Success| NEXT[Continue to Next Node]
    EXEC -->|Error| CHECK{Error Type?}

    CHECK -->|Rate Limit| WAIT[Wait 5s]
    CHECK -->|Auth Error| NOTIFY1[Notify: Check Credentials]
    CHECK -->|Timeout| RETRY{Retry Count < 3?}
    CHECK -->|No Data| PARTIAL[Continue with<br/>Partial Data]

    WAIT --> RETRY
    RETRY -->|Yes| EXEC
    RETRY -->|No| FALLBACK[Use Fallback<br/>or Skip]

    FALLBACK --> NEXT
    PARTIAL --> NEXT
    NOTIFY1 --> STOP[Stop Workflow]

    style START fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style EXEC fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style CHECK fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    style NEXT fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    style STOP fill:#ffcdd2,stroke:#c62828,stroke-width:2px
```

---

## 📊 Data Volume Visualization

```mermaid
graph LR
    subgraph IN["📥 INPUT"]
        I1[1 URL]
    end

    subgraph P1["PHASE 1"]
        P1_1[50 Keywords<br/>+ Metrics]
    end

    subgraph P2["PHASE 2"]
        P2_1[5 SERP Queries<br/>→ 50 Results]
        P2_2[3-5 Competitors<br/>Identified]
    end

    subgraph P3["PHASE 3"]
        P3_1[3 Competitor<br/>Profiles<br/>→ 90 Keywords]
        P3_2[15-20 Keyword<br/>Gaps Found]
    end

    subgraph P4["PHASE 4"]
        P4_1[Combined Dataset:<br/>~150 Data Points]
        P4_2[Claude Prompt:<br/>~15K Tokens]
        P4_3[Strategy Output:<br/>~5K Tokens]
    end

    subgraph OUT["📤 OUTPUT"]
        O1[Google Doc:<br/>8-12 Pages]
        O2[Google Sheet:<br/>5 Tabs,<br/>100+ Rows]
    end

    I1 --> P1_1
    P1_1 --> P2_1
    P2_1 --> P2_2
    P2_2 --> P3_1
    P3_1 --> P3_2
    P1_1 --> P4_1
    P2_2 --> P4_1
    P3_2 --> P4_1
    P4_1 --> P4_2
    P4_2 --> P4_3
    P4_3 --> O1
    P4_3 --> O2

    style IN fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style P1 fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style P2 fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style P3 fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style P4 fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style OUT fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

---

## 🎯 n8n Canvas Layout

```mermaid
graph LR
    subgraph COL1["Column 1<br/>INPUT"]
        N1[Webhook]
        N2[Respond]
        N3[Extract]
    end

    subgraph COL2["Column 2<br/>DISCOVERY"]
        N4[Keywords API]
        N5[Process]
        N6[Split]
    end

    subgraph COL3["Column 3<br/>SERP"]
        N7[SERP API]
        N8[Analyze]
        N9[Merge]
    end

    subgraph COL4["Column 4<br/>GAPS"]
        N10[Comp API]
        N11[Process]
        N12[Merge All]
    end

    subgraph COL5["Column 5<br/>AI"]
        N13[Prepare]
        N14[Claude]
    end

    subgraph COL6["Column 6<br/>OUTPUT"]
        N15[Docs]
        N16[Sheets]
        N17[Slack]
    end

    N1 --> N2
    N1 --> N3
    N3 --> N4
    N4 --> N5
    N5 --> N6
    N6 --> N7
    N7 --> N8
    N8 --> N9
    N9 --> N10
    N9 --> N12
    N10 --> N11
    N11 --> N12
    N12 --> N13
    N13 --> N14
    N14 --> N15
    N14 --> N16
    N15 --> N17
    N16 --> N17

    style COL1 fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    style COL2 fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style COL3 fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style COL4 fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style COL5 fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    style COL6 fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

---

## 🎨 Color Coding Guide

| Phase | Color | Purpose |
|-------|-------|---------|
| 🌐 **Input** | Blue | User interaction & webhook |
| 🔍 **Discovery** | Orange | Keyword discovery via API |
| 🎭 **SERP** | Purple | Search result analysis |
| 💎 **Gaps** | Green | Competitor & gap analysis |
| 🧠 **AI** | Teal | Claude AI processing |
| 📤 **Output** | Yellow | Final report generation |
| ✅ **Complete** | Light Green | Success state |
| ❌ **Error** | Red | Error states |

---

## 📱 Mobile-Friendly Summary Flow

```mermaid
graph TD
    A[📱 Enter URL] --> B[⚡ Auto-Magic!]
    B --> C[📊 Get Report]

    style A fill:#e1f5ff,stroke:#01579b,stroke-width:3px,color:#000
    style B fill:#fff3e0,stroke:#e65100,stroke-width:3px,color:#000
    style C fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px,color:#000
```

**For Solopreneurs:** It's literally this simple! 🚀
