# Design Patterns

125. Factory  

**Risposta:** Il Factory Pattern è un design pattern creazionale che permette di creare oggetti senza specificare la classe concreta. Questo pattern utilizza una classe Factory per creare oggetti di sottotipi di una classe comune. 

```Java
interface Shape {
    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Circle");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Square");
    }
}

class ShapeFactory {
    public Shape createShape(String type) {
        if (type.equals("Circle")) {
            return new Circle();
        } else if (type.equals("Square")) {
            return new Square();
        }
        return null;
    }
}

public class FactoryPattern {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();
        Shape circle = factory.createShape("Circle");
        circle.draw();

        Shape square = factory.createShape("Square");
        square.draw();
    }
}
```

126. Abstract factory  

**Risposta:** Il Abstract Factory Pattern è un design pattern creazionale che permette di creare famiglie di oggetti correlati senza specificare le classi concrete. Questo pattern fornisce un'interfaccia per creare oggetti di una famiglia e permette di sostituire facilmente una famiglia di oggetti con un'altra. 

```Java
interface Shape {
    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Circle");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Square");
    }
}

interface ShapeFactory {
    Shape createShape();
}

class CircleFactory implements ShapeFactory {
    @Override
    public Shape createShape() {
        return new Circle();
    }
}

class SquareFactory implements ShapeFactory {
    @Override
    public Shape createShape() {
        return new Square();
    }
}

public class AbstractFactoryPattern {
    public static void main(String[] args) {
        ShapeFactory circleFactory = new CircleFactory();
        Shape circle = circleFactory.createShape();
        circle.draw();

        ShapeFactory squareFactory = new SquareFactory();
        Shape square = squareFactory.createShape();
        square.draw();
    }
}
```

127. Builder  

**Risposta:** Il Builder Pattern è un design pattern creazionale che permette di costruire oggetti complessi passo dopo passo. Questo pattern separa la costruzione di un oggetto complesso dalla sua rappresentazione, consentendo di creare diversi tipi di oggetti utilizzando lo stesso processo di costruzione.$\\$
Spesso si utilizza l'ausilio di un Director per guidare il processo di costruzione e un Builder per costruire l'oggetto. 

```Java
class Car {
    private String make;
    private String model;
    private int year;

    public Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    public String getMake() {
        return make;
    }

    public String getModel() {
        return model;
    }

    public int getYear() {
        return year;
    }

    public String toString() {
        return "Car{" +
                "make='" + make + '\'' +
                ", model='" + model + '\'' +
                ", year=" + year +
                '}';
    }
}

interface CarBuilder {
    void setMake(String make);
    void setModel(String model);
    void setYear(int year);
    Car build();
}

class CarBuilderImpl implements CarBuilder {
    private Car car;

    public CarBuilderImpl() {
        this.car = new Car("default", "default", 0);
    }

    public void setMake(String make) {
        car = new Car(make, car.getModel(), car.getYear());
    }

    public void setModel(String model) {
        car = new Car(car.getMake(), model, car.getYear());
    }

    public void setYear(int year) {
        car = new Car(car.getMake(), car.getModel(), year);
    }

    public Car build() {
        return car;
    }
}

class CarDirector {
    private CarBuilder builder;

    public CarDirector(CarBuilder builder) {
        this.builder = builder;
    }

    public Car construct() {
        builder.setMake("Ford");
        builder.setModel("Mustang");
        builder.setYear(2020);
        return builder.build();
    }
}

public class Main {
    public static void main(String[] args) {
        CarBuilder builder = new CarBuilderImpl();
        CarDirector director = new CarDirector(builder);
        Car car = director.construct();
        System.out.println(car);
    }
}
```

In questo esempio, il Builder Pattern viene utilizzato per costruire un oggetto `Computer` passo dopo passo. Il `Director` guida il processo di costruzione utilizzando un `ComputerBuilder` specifico (`DesktopBuilder`) per costruire un computer desktop con specifiche personalizzate.

128. Prototype  

**Risposta:** Il Prototype Pattern è un design pattern creazionale che permette di creare nuovi oggetti duplicando un prototipo esistente. Questo pattern è utile quando la creazione di un oggetto è costosa o complessa e si desidera creare nuovi oggetti copiando un prototipo esistente. 

```Java
import java.util.HashMap;
import java.util.Map;

abstract class Shape implements Cloneable {
    protected String type;

    abstract void draw();

    public String getType() {
        return type;
    }

    @Override
    protected Object clone() {
        Object clone = null;
        try {
            clone = super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return clone;
    }
}

class Circle extends Shape {
    public Circle() {
        type = "Circle";
    }

    @Override
    void draw() {
        System.out.println("Circle");
    }
}

class Square extends Shape {
    public Square() {
        type = "Square";
    }

    @Override
    void draw() {
        System.out.println("Square");
    }
}

class ShapeCache {
    private static Map<String, Shape> shapeMap = new HashMap<>();

    public static Shape getShape(String type) {
        Shape cachedShape = shapeMap.get(type);
        return (Shape) cachedShape.clone();
    }

    public static void loadCache() {
        Circle circle = new Circle();
        shapeMap.put(circle.getType(), circle);

        Square square = new Square();
        shapeMap.put(square.getType(), square);
    }
}

public class PrototypePattern {
    public static void main(String[] args) {
        ShapeCache.loadCache();

        Shape clonedCircle = ShapeCache.getShape("Circle");
        System.out.println("Shape: " + clonedCircle.getType());

        Shape clonedSquare = ShapeCache.getShape("Square");
        System.out.println("Shape: " + clonedSquare.getType());
    }
}
```

In questo esempio, il Prototype Pattern viene utilizzato per creare nuovi oggetti `Circle` e `Square` duplicando un prototipo esistente. Il `ShapeCache` mantiene una mappa di prototipi e fornisce un metodo per ottenere un clone di un prototipo specifico.

129. Singleton  

**Risposta:** Il Singleton Pattern è un design pattern creazionale che permette di garantire che una classe abbia una sola istanza e fornisce un punto di accesso globale a tale istanza. Questo pattern è utile quando si desidera limitare il numero di istanze di una classe e fornire un modo per accedere a un'istanza condivisa. 

```Java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class SingletonPattern {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstance();
        Singleton singleton2 = Singleton.getInstance();

        System.out.println(singleton1 == singleton2); // true
    }
}
```

130. Adapter  

**Risposta:** Il Adapter Pattern è un design pattern strutturale che permette di convertire l'interfaccia di una classe in un'altra interfaccia che un cliente si aspetta. Questo pattern permette a classi con interfacce incompatibili di lavorare insieme. 

```Java
interface MediaPlayer {
    void play(String audioType, String fileName);
}

interface AdvancedMediaPlayer {
    void playVlc(String fileName);
    void playMp4(String fileName);
}

class VlcPlayer implements AdvancedMediaPlayer {
    @Override
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file: " + fileName);
    }

    @Override
    public void playMp4(String fileName) {
        // do nothing
    }
}

class Mp4Player implements AdvancedMediaPlayer {
    @Override
    public void playVlc(String fileName) {
        // do nothing
    }

    @Override
    public void playMp4(String fileName) {
        System.out.println("Playing mp4 file: " + fileName);
    }
}

class MediaAdapter implements MediaPlayer {
    private AdvancedMediaPlayer advancedMediaPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer = new VlcPlayer();
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer = new Mp4Player();
        }
    }

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer.playVlc(fileName);
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer.playMp4(fileName);
        }
    }
}

class AudioPlayer implements MediaPlayer {
    private MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file: " + fileName);
        } else if (audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media. " + audioType + " format not supported");
        }
    }
}

public class AdapterPattern {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.play("mp3", "song.mp3");
        audioPlayer.play("vlc", "movie.vlc");
        audioPlayer.play("mp4", "video.mp4");
        audioPlayer.play("avi", "video.avi");
    }
}
```
```java
interface Target {
    void request();
}

class Adaptee {
    public void specificRequest() {
        System.out.println("Specific request");
    }
}

class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public void request() {
        adaptee.specificRequest();
    }
}

public class Main {
    public static void main(String[] args) {
        Adaptee adaptee = new Adaptee();
        Target target = new Adapter(adaptee);
        target.request();
    }
}
```

In questo esempio, l'Adapter Pattern viene utilizzato per adattare le interfacce di `VlcPlayer` e `Mp4Player` all'interfaccia `MediaPlayer` utilizzata da `AudioPlayer`. L'`AudioPlayer` può riprodurre file mp3 direttamente e utilizza l'`MediaAdapter` per riprodurre file vlc e mp4.

131. Bridge  

**Risposta:** Il Bridge Pattern è un design pattern strutturale che permette di separare l'implementazione di un'astrazione dalla sua rappresentazione. Questo pattern consente di cambiare l'implementazione di un'astrazione senza modificare la sua interfaccia. 

```Java
interface Color {
    void applyColor();
}

class Red implements Color {
    @Override
    public void applyColor() {
        System.out.println("Red");
    }
}

class Blue implements Color {
    @Override
    public void applyColor() {
        System.out.println("Blue");
    }
}

abstract class Shape {
    protected Color color;

    public Shape(Color color) {
        this.color = color;
    }

    abstract void applyColor();
}

class Circle extends Shape {
    public Circle(Color color) {
        super(color);
    }

    @Override
    public void applyColor() {
        System.out.print("Circle filled with color ");
        color.applyColor();
    }
}

class Square extends Shape {
    public Square(Color color) {
        super(color);
    }

    @Override
    public void applyColor() {
        System.out.print("Square filled with color ");
        color.applyColor();
    }
}

public class BridgePattern {
    public static void main(String[] args) {
        Shape redCircle = new Circle(new Red());
        redCircle.applyColor();

        Shape blueSquare = new Square(new Blue());
        blueSquare.applyColor();
    }
}
```

In questo esempio, il Bridge Pattern viene utilizzato per separare l'implementazione di `Color` dall'implementazione di `Shape`. Le classi `Circle` e `Square` estendono `Shape` e utilizzano un'istanza di `Color` per applicare un colore specifico alla forma. Questo permette di cambiare facilmente il colore di una forma senza modificare la sua classe.

132. Composite 

**Risposta:** Il Composite Pattern è un design pattern strutturale che permette di trattare oggetti singoli e composizioni di oggetti in modo uniforme. Questo pattern permette di creare gerarchie di oggetti in modo flessibile e di trattare gli oggetti singoli e le composizioni di oggetti allo stesso modo. 

```Java
import java.util.ArrayList;
import java.util.List;

interface Graphic {
    void draw();
}

class Line implements Graphic {
    @Override
    public void draw() {
        System.out.println("Line");
    }
}

class Circle implements Graphic {
    @Override
    public void draw() {
        System.out.println("Circle");
    }
}

class Picture implements Graphic {
    private List<Graphic> graphics = new ArrayList<>();

    public void add(Graphic graphic) {
        graphics.add(graphic);
    }

    @Override
    public void draw() {
        for (Graphic graphic : graphics) {
            graphic.draw();
        }
    }
}

public class CompositePattern {
    public static void main(String[] args) {
        Graphic line = new Line();
        Graphic circle = new Circle();

        Picture picture = new Picture();
        picture.add(line);
        picture.add(circle);

        picture.draw();
    }
}
```

In questo esempio, il Composite Pattern viene utilizzato per creare una gerarchia di oggetti grafici (`Line`, `Circle`, `Picture`) e trattarli in modo uniforme. Il metodo `draw()` viene chiamato su un oggetto `Picture`, che a sua volta chiama `draw()` su tutti i suoi componenti (`Line` e `Circle`).

133. Decorator  

**Risposta:** Il Decorator Pattern è un design pattern strutturale che permette di aggiungere funzionalità a un oggetto in modo dinamico. Questo pattern consente di estendere le funzionalità di un oggetto senza modificare la sua struttura. 

```Java
interface Shape {
    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Circle");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Square");
    }
}

abstract class ShapeDecorator implements Shape {
    protected Shape shape;

    public ShapeDecorator(Shape shape) {
        this.shape = shape;
    }

    @Override
    public void draw() {
        shape.draw();
    }
}

class RedShapeDecorator extends ShapeDecorator {
    public RedShapeDecorator(Shape shape) {
        super(shape);
    }

    @Override
    public void draw() {
        shape.draw();
        setRedBorder();
    }

    private void setRedBorder() {
        System.out.println("Border Color: Red");
    }
}

public class DecoratorPattern {
    public static void main(String[] args) {
        Shape circle = new Circle();
        Shape redCircle = new RedShapeDecorator(new Circle());
        Shape redSquare = new RedShapeDecorator(new Square());

        circle.draw();
        redCircle.draw();
        redSquare.draw();
    }
}
```

134. Facade  

**Risposta:** Il Facade Pattern è un design pattern strutturale che fornisce un'interfaccia unificata per un insieme di interfacce in un sottosistema. Questo pattern permette di semplificare l'interazione con un sottosistema complesso fornendo un'interfaccia più semplice e unificata. 

```Java
class SubsystemA {
    public void operationA() {
        System.out.println("Subsystem A operation");
    }
}

class SubsystemB {
    public void operationB() {
        System.out.println("Subsystem B operation");
    }
}

class Facade {
    private SubsystemA subsystemA;
    private SubsystemB subsystemB;

    public Facade() {
        this.subsystemA = new SubsystemA();
        this.subsystemB = new SubsystemB();
    }

    public void operation() {
        subsystemA.operationA();
        subsystemB.operationB();
    }
}

public class FacadePattern {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.operation();
    }
}
```

135. Flyweight  

**Risposta:** Il Flyweight Pattern è un design pattern strutturale che permette di condividere oggetti per ridurre la memoria o il costo computazionale. Questo pattern è utile quando si desidera creare un gran numero di oggetti simili e si vuole ridurre il consumo di memoria o il costo computazionale. 

```Java
import java.util.HashMap;
import java.util.Map;

interface Shape {
    void draw();
}

class Circle implements Shape {
    private String color;

    public Circle(String color) {
        this.color = color;
    }

    @Override
    public void draw() {
        System.out.println("Circle: " + color);
    }
}

class ShapeFactory {
    private static final Map<String, Shape> shapes = new HashMap<>();

    public static Shape getCircle(String color) {
        Shape circle = shapes.get(color);

        if (circle == null) {
            circle = new Circle(color);
            shapes.put(color, circle);
        }

        return circle;
    }
}

public class FlyweightPattern {
    public static void main(String[] args) {
        Shape redCircle = ShapeFactory.getCircle("Red");
        redCircle.draw();

        Shape blueCircle = ShapeFactory.getCircle("Blue");
        blueCircle.draw();

        Shape redCircle2 = ShapeFactory.getCircle("Red");
        redCircle2.draw();
    }
}
```

In questo esempio, il Flyweight Pattern viene utilizzato per condividere oggetti `Circle` con lo stesso colore per ridurre il consumo di memoria. Il `ShapeFactory` mantiene una mappa di oggetti `Circle` e restituisce un oggetto esistente se è già stato creato con lo stesso colore.

136. Proxy  

**Risposta:** Il Proxy Pattern è un design pattern strutturale che permette di fornire un surrogato o un placeholder per un altro oggetto. Questo pattern consente di controllare l'accesso all'oggetto reale e di aggiungere funzionalità come il caching, la gestione delle autorizzazioni o il logging. 

```Java
interface Image {
    void display();
}

class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading " + filename);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + filename);
    }
}

class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}

public class ProxyPattern {
    public static void main(String[] args) {
        Image image = new ProxyImage("image.jpg");

        image.display();
        image.display();
    }
}
```

137. Chain of responsibilities  

**Risposta:** Il Chain of Responsibility Pattern è un design pattern comportamentale che permette di passare una richiesta tra una serie di oggetti per gestirla in modo flessibile. Questo pattern permette di separare il mittente di una richiesta dal suo destinatario, consentendo a più oggetti di gestire la richiesta in modo sequenziale o parallelo. 

```Java
abstract class Handler {
    protected Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    public abstract void handleRequest(int request);
}

class ConcreteHandler1 extends Handler {
    @Override
    public void handleRequest(int request) {
        if (request >= 0 && request < 10) {
            System.out.println("Handled by ConcreteHandler1");
        } else if (successor != null) {
            successor.handleRequest(request);
        }
    }
}

class ConcreteHandler2 extends Handler {
    @Override
    public void handleRequest(int request) {
        if (request >= 10 && request < 20) {
            System.out.println("Handled by ConcreteHandler2");
        } else if (successor != null) {
            successor.handleRequest(request);
        }
    }
}

public class ChainOfResponsibilityPattern {
    public static void main(String[] args) {
        Handler handler1 = new ConcreteHandler1();
        Handler handler2 = new ConcreteHandler2();

        handler1.setSuccessor(handler2);

        handler1.handleRequest(5);
        handler1.handleRequest(15);
    }
}
```

138. Command  

**Risposta:** Il Command Pattern è un design pattern comportamentale che permette di incapsulare una richiesta come un oggetto, consentendo di parametrizzare i client con richieste diverse, accodare richieste o registrare richieste per il ripristino. 

```Java
interface Command {
    void execute();
}

class Light {
    public void turnOn() {
        System.out.println("Light is on");
    }

    public void turnOff() {
        System.out.println("Light is off");
    }
}

class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }
}

class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOff();
    }
}

class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

public class CommandPattern {
    public static void main(String[] args) {
        Light light = new Light();
        Command lightOnCommand = new LightOnCommand(light);
        Command lightOffCommand = new LightOffCommand(light);

        RemoteControl remoteControl = new RemoteControl();
        remoteControl.setCommand(lightOnCommand);
        remoteControl.pressButton();

        remoteControl.setCommand(lightOffCommand);
        remoteControl.pressButton();
    }
}
```

In questo esempio, il Command Pattern viene utilizzato per incapsulare le operazioni di accensione e spegnimento di una luce come oggetti `LightOnCommand` e `LightOffCommand`. Un `RemoteControl` può essere configurato con uno di questi comandi e premere un pulsante per eseguire l'operazione corrispondente.

139. Iterator  

**Risposta:** L'Iterator Pattern è un design pattern comportamentale che permette di accedere agli elementi di una collezione senza esporre la sua rappresentazione interna. Questo pattern fornisce un modo standard per attraversare una collezione di oggetti in modo sequenziale. 

```Java
import java.util.ArrayList;
import java.util.List;

interface Iterator<T> {
    boolean hasNext();
    T next();
}

interface Aggregate<T> {
    Iterator<T> createIterator();
}

class ConcreteIterator<T> implements Iterator<T> {
    private List<T> list;
    private int position;

    public ConcreteIterator(List<T> list) {
        this.list = list;
        this.position = 0;
    }

    @Override
    public boolean hasNext() {
        return position < list.size();
    }

    @Override
    public T next() {
        return list.get(position++);
    }
}

class ConcreteAggregate<T> implements Aggregate<T> {
    private List<T> list;

    public ConcreteAggregate() {
        this.list = new ArrayList<>();
    }

    public void add(T element) {
        list.add(element);
    }

    @Override
    public Iterator<T> createIterator() {
        return new ConcreteIterator<>(list);
    }
}

public class IteratorPattern {
    public static void main(String[] args) {
        ConcreteAggregate<String> aggregate = new ConcreteAggregate<>();
        aggregate.add("A");
        aggregate.add("B");
        aggregate.add("C");

        Iterator<String> iterator = aggregate.createIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

140. Mediator  

**Risposta:** Il Mediator Pattern è un design pattern comportamentale che permette di ridurre le dipendenze tra i componenti di un sistema, promuovendo la comunicazione indiretta attraverso un oggetto Mediator centrale. Questo pattern facilita la gestione delle interazioni tra i componenti e promuove la modularità e la manutenibilità del sistema. 

```Java
import java.util.ArrayList;
import java.util.List;

interface Mediator {
    void sendMessage(String message, Colleague colleague);
}

abstract class Colleague {
    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }

    public abstract void receiveMessage(String message);
}

class ConcreteColleague extends Colleague {
    public ConcreteColleague(Mediator mediator) {
        super(mediator);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println("Received message: " + message);
    }

    public void sendMessage(String message) {
        mediator.sendMessage(message, this);
    }
}

class ConcreteMediator implements Mediator {
    private List<Colleague> colleagues;

    public ConcreteMediator() {
        this.colleagues = new ArrayList<>();
    }

    public void addColleague(Colleague colleague) {
        colleagues.add(colleague);
    }

    @Override
    public void sendMessage(String message, Colleague colleague) {
        for (Colleague c : colleagues) {
            if (c != colleague) {
                c.receiveMessage(message);
            }
        }
    }
}

public class MediatorPattern {
    public static void main(String[] args) {
        ConcreteMediator mediator = new ConcreteMediator();
        ConcreteColleague colleague1 = new ConcreteColleague(mediator);
        ConcreteColleague colleague2 = new ConcreteColleague(mediator);

        mediator.addColleague(colleague1);
        mediator.addColleague(colleague2);

        colleague1.sendMessage("Hello from colleague 1");
        colleague2.sendMessage("Hello from colleague 2");
    }
}
```

141. Memento  

**Risposta:** Il Memento Pattern è un design pattern comportamentale che permette di catturare e salvare lo stato di un oggetto in modo che possa essere ripristinato in un secondo momento. E' composto da tre componenti principali: l'Originator (l'oggetto di cui si vuole salvare lo stato), il Memento (l'oggetto che rappresenta lo stato dell'Originator) e il Caretaker (l'oggetto che gestisce i Memento). 

```Java
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }

    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
    }
}

class Caretaker {
    private List<Memento> mementoList = new ArrayList<>();

    public void addMemento(Memento memento) {
        mementoList.add(memento);
    }

    public Memento getMemento(int index) {
        return mementoList.get(index);
    }
}

public class MementoPattern {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State 1");
        originator.setState("State 2");
        caretaker.addMemento(originator.saveStateToMemento());

        originator.setState("State 3");
        caretaker.addMemento(originator.saveStateToMemento());

        System.out.println("Current State: " + originator.getState());

        originator.getStateFromMemento(caretaker.getMemento(0));
        System.out.println("First saved State: " + originator.getState());

        originator.getStateFromMemento(caretaker.getMemento(1));
        System.out.println("Second saved State: " + originator.getState());
    }
}
```

142. Observer  

**Risposta:** Il Observer Pattern è un design pattern comportamentale che permette a un oggetto (Subject) di notificare e aggiornare automaticamente una lista di oggetti dipendenti (Observers) quando il suo stato cambia. 

```Java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

class Subject {
    private List<Observer> observers = new ArrayList<>();
    private String message;

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void detach(Observer observer) {
        observers.remove(observer);
    }

    public void setMessage(String message) {
        this.message = message;
        notifyObservers();
    }

    private void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

class ConcreteObserver implements Observer {
    private String name;

    public ConcreteObserver(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received message: " + message);
    }
}

public class ObserverPattern {
    public static void main(String[] args) {
        Subject subject = new Subject();
        ConcreteObserver observer1 = new ConcreteObserver("Observer 1");
        ConcreteObserver observer2 = new ConcreteObserver("Observer 2");

        subject.attach(observer1);
        subject.attach(observer2);

        subject.setMessage("Hello World!");
    }
}
```

143. State  

**Risposta:** Il State Pattern è un design pattern comportamentale che permette a un oggetto di cambiare il suo comportamento quando il suo stato interno cambia. Questo pattern consente di incapsulare i diversi stati di un oggetto in classi separate e di delegare il comportamento a queste classi in base allo stato corrente. 

```Java
interface State {
    void doAction(Context context);
}

class StartState implements State {
    @Override
    public void doAction(Context context) {
        System.out.println("Player is in start state");
        context.setState(this);
    }

    @Override
    public String toString() {
        return "Start State";
    }
}

class StopState implements State {
    @Override
    public void doAction(Context context) {
        System.out.println("Player is in stop state");
        context.setState(this);
    }

    @Override
    public String toString() {
        return "Stop State";
    }
}

class Context {
    private State state;

    public Context() {
        state = null;
    }

    public void setState(State state) {
        this.state = state;
    }

    public State getState() {
        return state;
    }
}

public class StatePattern {
    public static void main(String[] args) {
        Context context = new Context();

        StartState startState = new StartState();
        startState.doAction(context);
        System.out.println(context.getState());

        StopState stopState = new StopState();
        stopState.doAction(context);
        System.out.println(context.getState());
    }
}
```

144. Strategy  

**Risposta:** Il Strategy Pattern è un design pattern comportamentale che permette di definire una famiglia di algoritmi, incapsularli e renderli intercambiabili. Questo pattern consente di selezionare dinamicamente l'algoritmo da utilizzare in base al contesto o ai requisiti specifici. 

```Java
interface Strategy {
    int doOperation(int num1, int num2);
}

class OperationAdd implements Strategy {
    @Override
    public int doOperation(int num1, int num2) {
        return num1 + num2;
    }
}

class OperationSubtract implements Strategy {
    @Override
    public int doOperation(int num1, int num2) {
        return num1 - num2;
    }
}

class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public int executeStrategy(int num1, int num2) {
        return strategy.doOperation(num1, num2);
    }
}

public class StrategyPattern {
    public static void main(String[] args) {
        Context context = new Context(new OperationAdd());
        System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

        context = new Context(new OperationSubtract());
        System.out.println("10 - 5 = " + context.executeStrategy(10, 5));
    }
}
```

145. Template  

**Risposta:** Il Template Pattern è un design pattern comportamentale che permette di definire lo scheletro di un algoritmo in una classe base e di lasciare che le sottoclassi implementino i passaggi specifici dell'algoritmo. Questo pattern promuove il riutilizzo del codice e permette di modificare il comportamento di un algoritmo senza modificare la sua struttura. 

```Java
abstract class Game {
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();

    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}

class Cricket extends Game {
    @Override
    void initialize() {
        System.out.println("Cricket Game Initialized! Start playing.");
    }

    @Override
    void startPlay() {
        System.out.println("Cricket Game Started. Enjoy the game!");
    }

    @Override
    void endPlay() {
        System.out.println("Cricket Game Finished!");
    }
}

class Football extends Game {
    @Override
    void initialize() {
        System.out.println("Football Game Initialized! Start playing.");
    }

    @Override
    void startPlay() {
        System.out.println("Football Game Started. Enjoy the game!");
    }

    @Override
    void endPlay() {
        System.out.println("Football Game Finished!");
    }
}

public class TemplatePattern {
    public static void main(String[] args) {
        Game cricket = new Cricket();
        cricket.play();

        Game football = new Football();
        football.play();
    }
}
```

146. Visitor

**Risposta:** Il Visitor Pattern è un design pattern comportamentale che permette di definire una nuova operazione senza modificare le classi degli oggetti su cui opera. Questo pattern consente di separare l'algoritmo dalla struttura dell'oggetto su cui opera, consentendo di aggiungere nuove operazioni senza modificare le classi esistenti. 

```Java
interface Visitor {
    void visit(Element element);
}

interface Element {
    void accept(Visitor visitor);
}

class ConcreteElementA implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }

    public String operationA() {
        return "ConcreteElementA operation";
    }
}

class ConcreteElementB implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }

    public String operationB() {
        return "ConcreteElementB operation";
    }
}

class ConcreteVisitor implements Visitor {
    @Override
    public void visit(Element element) {
        if (element instanceof ConcreteElementA) {
            System.out.println(((ConcreteElementA) element).operationA());
        } else if (element instanceof ConcreteElementB) {
            System.out.println(((ConcreteElementB) element).operationB());
        }
    }
}

public class VisitorPattern {
    public static void main(String[] args) {
        Element elementA = new ConcreteElementA();
        Element elementB = new ConcreteElementB();

        Visitor visitor = new ConcreteVisitor();
        elementA.accept(visitor);
        elementB.accept(visitor);
    }
}
```

In questo esempio, il Visitor Pattern viene utilizzato per definire un'operazione (`visit()`) che può essere applicata a diversi tipi di elementi (`ConcreteElementA`, `ConcreteElementB`) senza modificare le classi degli elementi stessi. Il Visitor (`ConcreteVisitor`) implementa l'operazione specifica per ciascun tipo di elemento.


# Altri codici

147. Polimorfismo ad hoc

**Risposta:** Il polimorfismo ad hoc è un tipo di polimorfismo che si basa sul concetto di overloading. In questo caso, il compilatore è in grado di selezionare la funzione giusta in base ai parametri passati. 

```Java
public class PolimorfismoAdHoc {
    public static void main(String[] args) {
        System.out.println(somma(1, 2));
        System.out.println(somma(1.0, 2.0));
    }

    public static int somma(int a, int b) {
        return a + b;
    }

    public static double somma(double a, double b) {
        return a + b;
    }
}
```

148. Polimorfismo ereditario

**Risposta:** Il polimorfismo ereditario è un tipo di polimorfismo che si basa sul concetto di ereditarietà e overriding. In questo caso, una classe figlia può sovrascrivere un metodo della classe padre e il metodo invocato dipenderà dal tipo dell'oggetto in esecuzione.

```Java
class PolimorfismoEreditario {
    public static void main(String[] args) {
        A a = new B();
        a.stampa(); // Stampa B
    }
}

class A {
    public void stampa() {
        System.out.println("A");
    }
}

class B extends A {
    @Override
    public void stampa() {
        System.out.println("B");
    }
}
```

149. Polimorfismo generico

**Risposta:** Il polimorfismo generico si riferisce all'uso di generici o template per creare codice che può funzionare con diversi tipi di dati. Questo permette di scrivere codice più flessibile e riutilizzabile.

```Java
class PolimorfismoGenerico {
    public static void main(String[] args) {
        Box<Integer> integerBox = new Box<>();
        integerBox.set(10);
        System.out.println(integerBox.get());

        Box<String> stringBox = new Box<>();
        stringBox.set("Hello");
        System.out.println(stringBox.get());
    }
}

class Box<T> {
    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}
```

150. Polimorfismo parametrico

**Risposta:** Il polimorfismo parametrico si riferisce all'uso di parametri di tipo generico per creare codice che può funzionare con diversi tipi di dati. Questo permette di scrivere codice più flessibile e riutilizzabile.

```Java
class PolimorfismoParametrico {
    public static void main(String[] args) {
        Pair<Integer, String> pair = new Pair<>(1, "One");
        System.out.println(pair.getKey() + ": " + pair.getValue());
    }
}

class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
}
```

# Domande da rifare

# Design Patterns

125. Factory
126. Abstract factory
127. Builder
128. Prototype
129. Singleton
130. Adapter
131. Bridge
132. Composite
133. Decorator
134. Facade
135. Flyweight
136. Proxy
137. Chain of responsibilities
138. Command
139. Iterator
140. Mediator
141. Memento
142. Observer
143. State
144. Strategy
145. Template
146. Visitor
147. Polimorfismo ad hoc
148. Polimorfismo ereditario
149. Polimorfismo generico
150. Polimorfismo parametrico