# Starbucks Bestellprozess (UML Sequenzdiagramm)


```mermaid
graph TD
    Start([Start]) --> Order[Customer says order]
    Order --> PutIn[Cashier puts order in Cash Register]
    PutIn --> Calc[Cash Register calculates price]
    Calc --> TellTotal[Cashier says total]
    TellTotal --> Tap[Customer taps card]
    Tap --> Process[Cashier makes payment]
    Process --> Auth[Cash Register requests authorization]
    Auth --> Check{Is Card Valid?}

    Check -- Yes --> Accept[Payment Provider accepts card]
    
    %% Hier starten BEIDE Aktionen gleichzeitig (Parallel)
    Accept --> SendOrder[Cash Register sends order to Barista]
    Accept --> Print[Cash Register prints receipt]
    
    %% Strang 1: Kassierer & Kunde
    Print --> GiveReceipt[Cashier gives receipt to Customer]
    GiveReceipt --> Wait[Customer waits for coffee]
    
    %% Strang 2: Barista
    SendOrder --> Make[Barista makes coffee]
    Make --> Pass[Barista passes coffee to Handler]
    
    %% Frühere Zusammenführung: Der wartende Kunde und der fertige Kaffee treffen sich
    Wait --> HandOver[Handler hands coffee to Customer]
    Pass --> HandOver
    
    HandOver --> Finish([Order Complete])
    
    %% Alternativer Strang (Abbruch)
    Check -- No --> Reject[Payment Provider rejects card]
    Reject --> RejectPay[Cash Register rejects payment]
    RejectPay --> Cancel[Cashier cancels order]
    
    Cancel --> FinishFailed([Order Cancelled])

