```mermaid
graph TD
    A[User Initiates Navigation Request]-->B{Real-time Detection Module}
    B-->C
    B-->D
    B-->E
    subgraph Parallel Analysis Engines
        C[Component 1: Heuristic Analysis Engine]
        D[Component 2: Graph-Based Behavior Analyzer]
        E[Component 3: Domain Reputation System]
    end
    C-->F{Aggregator / Meta-Classifier}
    D-->F
    E-->F
    F-->G{Verdict: Malicious?}
    G-->|Yes|H[Action: Block Navigation & Warn User]
    G-->|No|I[Action: Allow Navigation to Proceed]
    ```
