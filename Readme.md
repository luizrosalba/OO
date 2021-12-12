# Orientação a Objetos e Solid para ninjas - Design Patterns

Meus estudos usando o livro Orientação a Objetos e Solid para ninjas. 

Exemplos de Design Patterns do site https://www.javatpoint.com/

## Coesão 

Coesão = SRP 

Uma classe coesa é aquela que possui uma única responsabilidade 

Toda Classe que não é coesa não para de crescer nunca 

## Segregando responsabilidades 

Se quebramos um método grande em vários pequenos métodos privados não teremos reuso 
daquele comportamento isolado 

Se precisamos ficar buscaando todos os pontos onde a função é usada o código pode melhorar

O código deve estar amarrado ou seja, deve-se deixar claro os pontos que devem ser 
alterados no código ao se adicionar um comportamento (encapsulamento do problema )

## SRP 

Uma classe deve ter uma e apenas uma razão para mudar 

## Acoplamento 

Classes devem ser coesas e pouco acopladas

A partir do momento que uma classe depende de muitas outras classes, todas elas podem propagar problemas para a classe principal

Interfaces ajudam a criar módulos estáveis 

Acoplamento não é um problema se ocorre dependência de uma interface estável

## Princípio da inversão de dependência (DIP)

Sempre que uma classe for depender de outra ela deve depender sempre de outro módulo mais estável que ela mesma 


## Abstração 

A abstração consiste em um dos pontos mais importantes dentro de qualquer linguagem Orientada a Objetos. 
Como estamos lidando com uma representação de um objeto real (o que dá nome ao paradigma), 
temos que imaginar o que esse objeto irá realizar dentro de nosso sistema.

1) O primeiro ponto é darmos uma identidade ao objeto que iremos criar. Essa identidade deve ser única dentro do sistema para que não haja conflito. Na maior parte das linguagens, há o conceito de pacotes (ou namespaces). Nessas linguagens, a identidade do objeto não pode ser repetida dentro do pacote, e não necessariamente no sistema inteiro.
2) A segunda parte diz respeito a características do objeto. Como sabemos, no mundo real qualquer objeto possui elementos que o definem. Dentro da programação orientada a objetos, essas características são nomeadas propriedades. Por exemplo, as propriedades de um objeto “Cachorro” poderiam ser “Tamanho”, “Raça” e “Idade”.
3) Por fim, a terceira parte é definirmos as ações que o objeto irá executar. Essas ações, ou eventos, são chamados métodos. Esses métodos podem ser extremamente variáveis, desde “Acender()” em um objeto lâmpada até “Latir()” em um objeto cachorro.

EX: 
1) Implementação : gato cachorro e passaro Abstração: Animal 
2) Implementação : ISS, IPVA e IPTU Abstração: Imposto
3) Implementação : homem e mulher Abstração: Humanos

Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações 

Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações 

## Princípio aberto-fechado (OCP) 

Classes devem ser abertas para extensão e fechadas para modificação 

Uma classe não deve ser modificada o tempo todo 

Não há razão para mudar a classe abaixo, para mudar seu comportamento basta passarmos diferentes implementações de suas dependências no construtor.

As interfaces (abstracoes) TabelaDePreco e ServicoDeEntrega devem ser estáveis

```
public class CalculadoraDePrecos { 
    private TabelaDePreco tabela;
    private ServicoDeEntrega entrega;

    public CalculadoraDePrecos(
        TabelaDePreco tabela, 
        ServicoDeEntrega entrega){

        this.tabela = tabela; 
        this.entrega = entrega;
    }
    // Nao instanciamos as deps apenas usamos

    public double calcula (Compra produto) {
        double desconto = 
            tabela.descontoPara(produto.getValor());
        double frete = entrega.para(produto.getCidade());
        return produto.getValor() * (1-desconto) + frete; 

    }

}
```

Poderiamos também injetar as dependecias usando métodos get e set entretanto usar o 
construtor obriga a passagem de dependências no momento da criação do objeto

## Encapsulamento 

A classe deve esconder os detalhes da implementação, ou seja como o método faz o seu trabalho. 


Ex: A classe ProcessadorDeBoletos não deve ter lógica de nota fiscal (intimidade inapropriada). Toda lógica de nota fiscal deve ficar na classe NotaFiscal

## Tell don't ask

Devemos dizer ao objeto o que fazer e não perguntar algo a ele para depois decidir. 

```
NotaFiscal nf = new NotaFiscal();
double valor = nf.calculaValorImpostos();
```

pág 70

## Padrões de projeto - Design Patterns 

https://www.javatpoint.com/

A design patterns are well-proved solution for solving the specific problem/task. (https://www.javatpoint.com/design-patterns-in-java)

1) Creational 
2) Structural
3) Behavioral

## 1 - Creational 

### Factory 

Problem: Suppose you want to create a class for which only 
a single instance (or object) should be created and that single object can be used by all other classes.


A Factory Pattern or Factory Method Pattern says that just define an interface or abstract class for creating an object but let the subclasses decide 
which class to instantiate. In other words, subclasses are responsible to create the instance of the class.

The Factory Method Pattern is also known as Virtual Constructor.

Advantage of Factory Design Pattern

Factory Method Pattern allows the sub-classes to choose the type of objects to create.

It promotes the loose-coupling by eliminating the need to bind application-specific classes into the code. 
That means the code interacts solely with the resultant interface or abstract class, 
so that it will work with any classes that implement that interface or that extends that abstract class.

Usage of Factory Design Pattern

- When a class doesn't know what sub-classes will be required to create
- When a class wants that its sub-classes specify the objects to be created.
- When the parent classes choose the creation of objects to its sub-classes.

```
class DogFactory
{
  public static Dog getDog(String criteria)
  {
    if ( criteria.equals("small") )
      return new Poodle();
    else if ( criteria.equals("big") )
      return new Rottweiler();
    else if ( criteria.equals("working") )
      return new SiberianHusky();

    return null;
  }
}
```

The factory doesn’t say it's returning a Poodle, Rottweiler, or SiberianHusky — 
it just says it's returning something that implements the Dog interface.

### Abstract Factory

Abstract Factory Pattern says that just define an interface or abstract class 
for creating families of related (or dependent) objects but without specifying their 
concrete sub-classes.That means Abstract Factory lets a class returns a factory of classes. 
So, this is the reason that Abstract Factory Pattern is one level higher than the Factory Pattern.

An Abstract Factory Pattern is also known as Kit.

Advantage of Abstract Factory Pattern

- Abstract Factory Pattern isolates the client code from concrete (implementation) classes.
- It eases the exchanging of object families.
- It promotes consistency among objects.

Usage of Abstract Factory Pattern

- When the system needs to be independent of how its object are created, composed, and represented.
- When the family of related objects has to be used together, then this constraint needs to be enforced.
- When you want to provide a library of objects that does not show implementations and only reveals interfaces.
- When the system needs to be configured with one of a multiple family of objects.


### Singleton 

Singleton Pattern says that just"define a class that has only one instance and provides a global point of access to it".

In other words, a class must ensure that only single instance should be created and single object can be used by all other classes.

There are two forms of singleton design pattern

Early Instantiation: creation of instance at load time.

Lazy Instantiation: creation of instance when required.

Advantage of Singleton design pattern

    Saves memory because object is not created at each request. Only single instance is reused again and again.

Usage of Singleton design pattern

Singleton pattern is mostly used in multi-threaded and database applications. It is used in logging, caching, thread pools, configuration settings etc.

How to create Singleton design pattern?

To create the singleton class, we need to have static member of class, private constructor and static factory method.

- Static member: It gets memory only once because of static, itcontains the instance of the Singleton class.
- Private constructor: It will prevent to instantiate the Singleton class from outside the class.
- Static factory method: This provides the global point of access to the Singleton object and returns the instance to the caller.

Understanding early Instantiation of Singleton Pattern

In such case, we create the instance of the class at the time of declaring the static data member, so instance of the class is created at the time of classloading.

Let's see the example of singleton design pattern using early instantiation.

```
class A{  
    private static A obj=new A();//Early, instance will be created at load time  
    private A(){}  
    
    public static A getA(){  
    return obj;  
    }  
    
    public void doSomething(){  
    //write your code  
    }  
}  
```

Understanding lazy Instantiation of Singleton Pattern

In such case, we create the instance of the class in synchronized method or synchronized block, so instance of the class is created when required.

Let's see the simple example of singleton design pattern using lazy instantiation.

```
class A{  
 private static A obj;  
 private A(){}  
   
 public static A getA(){  
   if (obj == null){  
      synchronized(Singleton.class){  
        if (obj == null){  
            obj = new Singleton();//instance will be created at request time  
        }  
    }              
    }  
  return obj;  
 }  
  
 public void doSomething(){  
 //write your code  
 }  
}  
```

### Prototype 

Prototype Pattern says that cloning of an existing object instead of creating new 
one and can also be customized as per the requirement.

This pattern should be followed, if the cost of creating a new object is expensive and resource intensive.

Advantage of Prototype Pattern

The main advantages of prototype pattern are as follows:

- It reduces the need of sub-classing.
- It hides complexities of creating objects.
- The clients can get new objects without knowing which type of object it will be.
- It lets you add or remove objects at runtime.

Usage of Prototype Pattern

- When the classes are instantiated at runtime.
- When the cost of creating an object is expensive or complicated.
- When you want to keep the number of classes in an application minimum.
- When the client application needs to be unaware of object creation and representation.


### Builder 

Builder Pattern says that "construct a complex object from simple objects using step-by-step approach"

It is mostly used when object can't be created in single step like in the de-serialization of a complex object.

Advantage of Builder Design Pattern

The main advantages of Builder Pattern are as follows:

- It provides clear separation between the construction and representation of an object.
- It provides better control over construction process.
- It supports to change the internal representation of objects.

### Object Pool 

Mostly, performance is the key issue during the software development and the object creation, which may be a costly step.

Object Pool Pattern says that " to reuse the object that are expensive to create".

Basically, an Object pool is a container which contains a specified amount of objects. 
When an object is taken from the pool, it is not available in the pool until it is put back. 
Objects in the pool have a lifecycle: creation, validation and destroy.

A pool helps to manage available resources in a better way. 
There are many using examples: especially in application servers there are data source pools, 
thread pools etc.

Advantage of Object Pool design pattern

- It boosts the performance of the application significantly.
- It is most effective in a situation where the rate of initializing a class instance is high.
- It manages the connections and provides a way to reuse and share them.
- It can also provide the limit for the maximum number of objects that can be created.

Usage:

- When an application requires objects which are expensive to create. Eg: there is a need of opening too many connections for the database then it takes too longer to create a new one and the database server will be overloaded.
- When there are several clients who need the same resource at different times.

## 2) Structural Pattern

### Adapter 

An Adapter Pattern says that just "converts the interface of a class into another interface that a client wants".

In other words, to provide the interface according to client requirement 
while using the services of a class with a different interface.

The Adapter Pattern is also known as Wrapper.

Advantage of Adapter Pattern

- It allows two or more previously incompatible objects to interact.
- It allows reusability of existing functionality.

Usage of Adapter pattern:

It is used:

- When an object needs to utilize an existing class with an incompatible interface.
- When you want to create a reusable class that cooperates with classes which don't have compatible interfaces.

### Bridge 

A Bridge Pattern says that just "decouple the functional abstraction from the implementation 
so that the two can vary independently".

The Bridge Pattern is also known as Handle or Body.

Advantage of Bridge Pattern

- It enables the separation of implementation from the interface.
- It improves the extensibility.
- It allows the hiding of implementation details from the client.

Usage of Bridge Pattern

- When you don't want a permanent binding between the functional abstraction and its implementation.
- When both the functional abstraction and its implementation need to extended using sub-classes.
- It is mostly used in those places where changes are made in the implementation does not affect the clients.


https://www.javatpoint.com/bridge-pattern 

### Composite 

A Composite Pattern says that just "allow clients to operate in generic manner 
on objects that may or may not represent a hierarchy of objects".

Advantage of Composite Design Pattern

- It defines class hierarchies that contain primitive and complex objects.
- It makes easier to you to add new kinds of components.
- It provides flexibility of structure with manageable class or interface.
Usage of Composite Pattern :

- When you want to represent a full or partial hierarchy of objects.
- When the responsibilities are needed to be added dynamically 
to the individual objects without affecting other objects. Where the responsibility 
of object may vary from time to time.

### Decorator 

A Decorator Pattern says that just "attach a flexible additional responsibilities 
to an object dynamically".

In other words, The Decorator Pattern uses composition instead of inheritance 
to extend the functionality of an object at runtime.

The Decorator Pattern is also known as Wrapper.

Advantage of Decorator Pattern

- It provides greater flexibility than static inheritance.
- It enhances the extensibility of the object, because changes are made by coding new classes.
- It simplifies the coding by allowing you to develop a series of functionality from targeted classes instead of coding all of the behavior into the object.

Usage of Decorator Pattern

- When you want to transparently and dynamically add responsibilities to objects without affecting other objects.
- When you want to add responsibilities to an object that you may want to change in future.
- Extending functionality by sub-classing is no longer practical.

### Facade 

A Facade Pattern says that just "just provide a unified and simplified interface 
to a set of interfaces in a subsystem, therefore it hides the complexities of the 
subsystem from the client".

In other words, Facade Pattern describes a higher-level interface 
that makes the sub-system easier to use.

Practically, every Abstract Factory is a type of Facade.

Advantage of Facade Pattern

- It shields the clients from the complexities of the sub-system components.
- It promotes loose coupling between subsystems and its clients.

Usage of Facade Pattern:

- When you want to provide simple interface to a complex sub-system.
- When several dependencies exist between clients and the implementation classes of an abstraction.

### Flyweigth 

A Flyweight Pattern says that just "to reuse already existing similar 
kind of objects by storing them and create new object when no matching object is found".

Advantage of Flyweight Pattern

- It reduces the number of objects.
- It reduces the amount of memory and storage devices required if the objects are persisted

Usage of Flyweight Pattern

- When an application uses number of objects
- When the storage cost is high because of the quantity of objects.
- When the application does not depend on object identity.

### Proxy 

Simply, proxy means an object representing another object.

According to GoF, a Proxy Pattern "provides the control for accessing the original object".

So, we can perform many operations like hiding the information of original object, 
on demand loading etc.

Proxy pattern is also known as Surrogate or Placeholder.

Advantage of Proxy Pattern

It provides the protection to the original object from the outside world.

Usage of Proxy Pattern:

- It can be used in Virtual Proxy scenario---Consider a situation where there is multiple database call to extract huge size image. Since this is an expensive operation so here we can use the proxy pattern which would create multiple proxies and point to the huge size memory consuming object for further processing. The real object gets created only when a client first requests/accesses the object and after that we can just refer to the proxy to reuse the object. This avoids duplication of the object and hence saving memory.
- It can be used in Protective Proxy scenario---It acts as an authorization layer to verify that whether the actual user has access the appropriate content or not. For example, a proxy server which provides restriction on internet access in office. Only the websites and contents which are valid will be allowed and the remaining ones will be blocked.
- It can be used in Remote Proxy scenario---A remote proxy can be thought about the stub in the RPC call. The remote proxy provides a local representation of the object which is present in the different address location. Another example can be providing interface for remote resources such as web service or REST resources.
- It can be used in Smart Proxy scenario---A smart proxy provides additional layer of security by interposing specific actions when the object is accessed. For example, to check whether the real object is locked or not before accessing it so that no other objects can change it.

## 3) Behavioral

### Chain of responsability 

In chain of responsibility, sender sends a request to a chain of objects. 
The request can be handled by any object in the chain.

A Chain of Responsibility Pattern says that just 
"avoid coupling the sender of a request to its receiver by 
giving multiple objects a chance to handle the request". 
For example, an ATM uses the Chain of Responsibility design pattern in money giving process.

In other words, we can say that normally each receiver contains 
reference of another receiver. If one object cannot handle the request 
then it passes the same to the next receiver and so on.

Advantage of Chain of Responsibility Pattern

- It reduces the coupling.
- It adds flexibility while assigning the responsibilities to objects.
- It allows a set of classes to act as one; events produced in one class can be sent to other handler classes with the help of composition.

Usage of Chain of Responsibility Pattern:

- When more than one object can handle a request and the handler is unknown.
- When the group of objects that can handle the request must be specified in dynamic way.

### Command 

A Command Pattern says that "encapsulate a request under an object as a
command and pass it to invoker object. Invoker object looks for the appropriate 
object which can handle this command and pass the command to the corresponding object 
and that object executes the command".

It is also known as Action or Transaction.

Advantage of command pattern

- It separates the object that invokes the operation from the object that actually performs the operation.
- It makes easy to add new commands, because existing classes remain unchanged.

Usage of command pattern:

- When you need parameterize objects according to an action perform.
- When you need to create and execute requests at different times.
- When you need to support rollback, logging or transaction functionality.

### Interpreter 

An Interpreter Pattern says that "to define a representation of grammar of a given language, 
along with an interpreter that uses this representation to interpret sentences in the language".

Basically the Interpreter pattern has limited area where it can be applied. 
We can discuss the Interpreter pattern only in terms of formal grammars but in 
this area there are better solutions that is why it is not frequently used.

This pattern can applied for parsing the expressions defined in simple grammars 
and sometimes in simple rule engines.

Advantage of Interpreter Pattern

- It is easier to change and extend the grammar.
- Implementing the grammar is straightforward.

Usage of Interpreter pattern:

- When the grammar of the language is not complicated.
- When the efficiency is not a priority.

### Iterator 

According to GoF, Iterator Pattern is used "to access the elements of an aggregate 
object sequentially without exposing its underlying implementation".

The Iterator pattern is also known as Cursor.

In collection framework, we are now using Iterator that is preferred over Enumeration.

java.util.Iterator interface uses Iterator Design Pattern.

Advantage of Iterator Pattern

- It supports variations in the traversal of a collection.
- It simplifies the interface to the collection.

Usage of Iterator Pattern:

- When you want to access a collection of objects without exposing its internal representation.
- When there are multiple traversals of objects need to be supported in the collection.

### Mediator 

A Mediator Pattern says that "to define an object that encapsulates how a set of objects interact".

I will explain the Mediator pattern by considering a problem. 
When we begin with development, we have a few classes and these classes interact 
with each other producing results. Now, consider slowly, the logic becomes 
more complex when functionality increases. Then what happens? 
We add more classes and they still interact with each other but it gets really difficult 
to maintain this code now. So, Mediator pattern takes care of this problem.

Mediator pattern is used to reduce communication complexity between multiple objects or classes. 
This pattern provides a mediator class which normally handles all the communications between
 different classes and supports easy maintainability of the code by loose coupling.

Benefits:

- It decouples the number of classes.
- It simplifies object protocols.
- It centralizes the control.
- The individual components become simpler and much easier to deal with because they don't need to pass messages to one another.
- The components don't need to contain logic to deal with their intercommunication and therefore, they are more generic.

Usage:

- It is commonly used in message-based systems likewise chat applications.
- When the set of objects communicate in complex but in well-defined ways.

### Memento 

A Memento Pattern says that "to restore the state of an object to its previous state". 
But it must do this without violating Encapsulation. 
Such case is useful in case of error or failure.

The Memento pattern is also known as Token.

Undo or backspace or ctrl+z is one of the most used operation in an editor. 
Memento design pattern is used to implement the undo operation. 
This is done by saving the current state of the object as it changes state.




### Observer


### Visitor 







