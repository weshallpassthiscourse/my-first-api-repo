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
    
    Accept --> SendOrder[Cash Register sends order to Barista]
    Accept --> Print[Cash Register prints receipt]
    
    Print --> GiveReceipt[Cashier gives receipt to Customer]
    
    SendOrder --> Make[Barista makes coffee]
    Make --> Pass[Barista passes coffee to Handler]
    Pass --> HandOver[Handler hands coffee to Customer]
    
    HandOver --> Finish([Order Complete])

    Check -- No --> Reject[Payment Provider rejects card]
    Reject --> RejectPay[Cash Register rejects payment]
    RejectPay --> Cancel[Cashier cancels order]
    
    Cancel --> FinishFailed([Order Cancelled])
