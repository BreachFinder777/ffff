flowchart TD
    B[Start] --> C_SubGraph
    B --> D_SubGraph
    B --> E_SubGraph
    
    subgraph C_SubGraph [Component 1: Heuristic Analysis Engine]
        direction TB
        C1[1. Extract Lexical & Host-Based Features]
        C2["- URL Length<br/>- Subdomain Count<br/>- Special Char Count<br/>- URL Entropy<br/>- Suspicious Keywords"]
        C3[2. Apply Pre-trained Random Forest Classifier]
        C4[Output: Heuristic Risk Score]
        C1 --> C2 --> C3 --> C4
    end
    
    subgraph D_SubGraph [Component 2: Graph-Based Behavior Analyzer]
        direction TB
        D1{Is it an HTTP Redirect?}
        D2[1. Monitor Sequence & Construct<br/>Redirect Chain Graph RCG]
        D3[2. Analyze Topological Features]
        D4["- Chain Length<br/>- Node Count<br/>- Graph Density<br/>- Subgraph Count"]
        D5[3. Apply Anomaly Detection Model]
        D6[Output: Behavioral Risk Score]
        D_End((No Redirect))
        D1 -- Yes --> D2 --> D3 --> D4 --> D5 --> D6
        D1 -- No --> D_End
    end
    
    subgraph E_SubGraph [Component 3: Domain Reputation System]
        direction TB
        E1[1. Extract Unique Domains from URL & Chain]
        E2[2. Aggregate Data via Parallel API Queries]
        E3["- Threat Intel Feeds: Spamhaus, OpenPhish<br/>- Multi-Scanner: VirusTotal<br/>- Domain Provenance: WHOIS Age<br/>- Hosting Infrastructure: IP-to-ASN, Passive DNS"]
        E4[3. Apply Weighted Scoring Algorithm]
        E5[Output: Reputation Score]
        E1 --> E2 --> E3 --> E4 --> E5
    end
    
    C4 --> F
    D6 --> F
    D_End --> F
    E5 --> F{Final Aggregator / Meta-Classifier}
    
    F -- Aggregates Scores & Generates Verdict --> G{Final Verdict: Malicious?}
    
    G -- Yes --> H["Action: Block Navigation<br/>Display Warning to User"]
    G -- No --> I[Action: Allow Navigation to Proceed]
