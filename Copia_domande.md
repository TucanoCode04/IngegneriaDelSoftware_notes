### **Modulo 1**
#### Da ripetere
1. Cos'è il Modello a spirale? [x]
2. Quali sono i principi agili e l'etica del movimento Agile? [x]
3. Cos'è Essence? [x]
4. Quali sono i principi INVEST? [x]
5. Qual è la differenza tra User Stories orizzontali e verticali? [x]
6. Differenze tra casi d'uso e User Stories? [x]
7. Cosa si intende per valore, produttività, costo e debito tecnico? [x]
8. Cosa sono i Function Points (FP)? 
9. Cos'è il modello COCOMO?
10. Quali sono i metodi di testing? [x]
11. Qual è il Goal Question Metric (GQM)? [x]
12. Quali sono le metriche di manutenibilità? [x]

### **Modulo 2**
#### Da ripetere assolutamente
1. Cos'è il metodo ROOM? [x]

#### Da ripetere
1. Cos'è l'analisi e progettazione di sistemi in tempo reale? (con esempi) [x]
2. Cos'è OCL (Object Constraint Language)? [x] (da rivedere)
3. Cos'è un ADT (Abstract Data Type)? [x] (da rivedere con codice)
4. Cos'è l'Event-driven control? [x]
5. Cos'è il Data flow model? [x]
6. Cos'è il modello a oggetti (OO model)? [x]
7. Cosa sono le architetture a N-tiers (multilivello)? [x]
8. Cos'è il controllo centralizzato? [x]
9. Cos'è RTTI (Run-Time Type Information) in C vs in Java? [x]
10. Cosa sono le eccezioni (Exception)? [x] (da rivedere)
11. Come gestisce Java le eccezioni? [x]

### **Modulo 3**
#### Da ripetere
1. Cosa sono le classi anonime? [x]
2. Come funziona l'ereditarietà in Python? [x]
3. Cos'è il reflection e quali sono le primitive di reflection? [x]
4. Cosa si intende per "referenza al clone design pattern"? [x]
5. Come avviene l'instanziazione di nuovi tipi? [x]
6. Come funziona la creazione di un oggetto con le metaclassi? [x]
7. Come si utilizza type come metaclasse? [x]
8. Cosa sono le metaclassi? [x]
9. Cos'è il template pattern con le metaclassi? [x]
10. Come si generalizza il singleton pattern? [x]

### **UML**
#### Da ripetere
1. Cosa rappresenta un Class Diagram? [x]
2. Cos'è un Use Case Diagram? [x]
3. Cos'è un Statechart Diagram? [x]
4. Cos'è un Activity Diagram? [x]
5. Cos'è un Sequence Diagram? [x]
6. Cos'è un Collaboration Diagram? [x]
7. Cos'è un Package Diagram? [x]
8. Cos'è un Components Diagram? [x]

#### Extra
1. Qual è la suddistinzione?

**Risposta:** I diagrammi UML sono suddivisi in 2 categorie:
- Diagrammi strutturali:
    - Class Diagram
    - Object Diagram
    - Component Diagram
    - Composite Structure Diagram
    - Package Diagram
    - Deployment Diagram
- Diagrammi comportamentali:
    - Use Case Diagram
    - Activity Diagram
    - State Machine Diagram
    - Sequence Diagram
    - Communication Diagram
    - Interaction Overview Diagram
    - Timing Diagram

### **Design patterns**
#### Da ripetere
1. Cos'è il pattern Factory? [x]
2. Cos'è l'Abstract Factory pattern? [x] 
3. Cos'è il Builder pattern? [x] (1 errore)
4. Cos'è il Prototype pattern? [x] (metà sbagliata)
5. Cos'è il Singleton pattern? [x]
6. Cos'è l'Adapter pattern? [x] (1 errore)
7. Cos'è il Bridge pattern? [x] (1 errore)
8. Cos'è il Composite pattern? [x] (non mi ricordavo cosa fosse)
9. Cos'è il Decorator pattern? [x] (metà sbagliata)
10. Cos'è il Facade pattern? [x] (non mi ricordavo cosa fosse)
11. Cos'è il Flyweight pattern? [x] (1 errore)
12. Cos'è il Proxy pattern? [x] (1 errore)
13. Cos'è il Chain of Responsibility pattern? [x] (1 errore)
14. Cos'è il Command pattern? [x] (1 errore)
15. Cos'è l'Iterator pattern? [x] (1 errore)
16. Cos'è il Mediator pattern? [x] (metà sbagliata)
17. Cos'è il Memento pattern? [x] (1 errore)
18. Cos'è l'Observer pattern? [x] (1 errore)
19. Cos'è il State pattern? [x] (metà sbagliata)
20. Cos'è il Strategy pattern? [x] (1 errore)
21. Cos'è il Template pattern? [x]
22. Cos'è il Visitor pattern? [x] (1 errore)
23. Cos'è il polimorfismo ad hoc? [x] (non mi ricordavo cosa fosse)
24. Cos'è il polimorfismo ereditario? [x] (non mi ricordavo cosa fosse)
25. Cos'è il polimorfismo generico? [x] (non mi ricordavo cosa fosse)
26. Cos'è una funzione virtuale?
27. Cos'è una funzione astraatta?

#### Extra
1. Qual è la suddistinzione?

**Risposta:** I Design Patterns sono suddivisi in 3 categorie: 
- creazionali(ossia quelli che si occupano della creazione di oggetti):
    - Factory Method: si ha un interfaccia che dev'esser eimplementata. E una factory con degli if
    - Abstract Factory: si ha un interfaccia che dev'esser eimplementata. E un interfaccia factory che dev'esser implementata
    - Builder: c'è una classe, un'altra classe che la costruisce e un director che ha un metodo per costruire un oggetto specifico
    - Prototype: si implementa una classe astratta implementando cloneable, e si tiene una cache di oggetti
    - Singleton: si ha un costruttore privato e un metodo statico per ottenere l'istanza
- strutturali(ossia quelli che si occupano della composizione di classi e oggetti):
    - Adapter: devi passare dal target all'adaptee, implementi il target faendo l'adaptor
    - Bridge: implementor e abstraction, implementor ha un metodo implementoperation e abstraction ha un metodo operation
    - Composite: linea e cerchio implementano graphic e il compsite implementa graphic che drawa tutto
    - Decorator: implementare un interfaccia shape, una classe astratta decorator che implementa shape e un red decorator
    - Facade: ci sono die subsystem e una facade che li chiama
    - Flyweight: c'è un interfaccia da implementare e si tiene una lista di oggetti da replicare
    - Proxy: c'è la real image e la fake image
- comportamentali(ossia quelli che si occupano della comunicazione tra oggetti):
    - Chain of Responsibility: c'è una classe astratta che dev'esser implementata e vari handler che la implementano
    - Command: c'è la luce, i comanid light on e light off che che implementano command. E c'è un remote con i comandi
    - Iterator: c'è un iterator d aimplementare che ha un metodo next e hasnext. C'è un aggregate che ha un metodo create iterator con una lista di elementi da passargli
    - Mediator: c'è un mediator che ha una lista di collega e un metodo per mandare un messaggio. i singoli collega hanno un metodo per ricevere il messaggio
    - Memento: memento, caretaker(ha la lista di memento) e originator(chiama il memento col so stato)
    - Observer: c'è un subject che ha una lista di observer e un metodo per aggiungere e rimuovere observer. E c'è un observer che implementa update
    - State: interfaccia stato, implementata da vari stati con delle azioni che prendono come parametro il contesto. Il contesto ha uno stato e un metodo per cambiare stato
    - Strategy: interfaccia strategy e add che impelementa strategy. E c'è un context che ha una strategy
    - Template: c'è una classe astratta che deve essere implementata da una sottoclasse
    - Visitor: un visitor vista un elemento e fa la sua operazione, c'è un elemento che accetta il visitor e fa qualche operazione.


