# P.O.O
Anotações de aula referente a Programação Orientada a Objetos em Java

## Ambiente de execução

Java Development Kit (JDK): compilador, interpretador e bibliotecas

Java Runtime Environment (JRE): apenas para execução

Várias implementações: Oracle, OpenJDK, Azul, etc.

Gerenciadores de projetos/dependências: Maven, Gradle, etc.

Em nuvem: Repl.it, GDB online, Python Tutor

## Conceitos Iniciais
### 1. Abstração
Simplificação de sistemas complexos em partes menores e mais gerenciáveis.

### 2. Encapsulamento
Agrupamento de dados (atributos) e métodos que operam nesses dados em uma única unidade ou classe.

#### Exemplo de recurso de implementação: Classe (Representa definição de novo tipo)

```Java
class Circle {
  private double x; // atributo, com visibilidade privada, ou seja, indica acesso permitido somente em código interno à própria classe
  private double y; // atributo
  private double r; // atributo
  public double area() { // método, com visibilidade pública, ou seja, indica acesso permitido fora da classe
     return 3.1416 * r * r;
  }
}
```

##### Instância de uma classe: Objeto (Alocado em memória e referenciado por um nome)

```Java
class TestCircle {
  public static void main(String[] args) {
    // declara a variável c como referência para um objeto da classe Circle
    Circle c;
    // cria objeto da classe Circle e guarda referência em c
    c = new Circle(); 
    // chama método area() do objeto referenciado por c
    System.out.println(c.area());
    // forma abreviada:
    // Circle c1 = new Circle(); 
  }
}
```

##### Código que inicializa objeto: Construtor

```Java
class Circle {
  private double x, y, r;

  // construtor default, sem argumentos
  public Circle() {
    x = y = 0.0;
    r = 1.0;
  }

  public double area() {
    return 3.1416 * r * r;
  }
}
class TestCircle {
  public static void main(String[] args) {
    // construtor chamado aqui
    Circle c = new Circle(); 
    System.out.println(c.area());    
  }
}
```

```Java
class Person {
  private String name;
  public Person() {
    System.out.println("Construtor de Person");
  }
  public String getName() {
    return this.name;
  }
}

class Student extends Person {
  private String course;
  public Student() {
    System.out.println("Construtor de Student");
  }
}

class Main {
  public static void main(String[] args) {
    // chama construtor de Person e depois de Student
    Student s = new Student();
  }
}
```
##### Visibilidade protected
Torna atributos e métodos visíveis a classes derivadas (mas não a outras classes "fora da família")

```Java
class Person {
  protected String name; // agora é protected!
  public Person() {
    System.out.println("Construtor de Person");
  }
  public String getName() {
    return this.name;
  }
}

class Student extends Person {
  private String course;
  public Student() {
    System.out.println("Construtor de Student");
    this.course = "CC";
    this.name = ""; // OK agora!
  }
}
```

### 3. Herança
Subclasses herdam atributos e métodos já existentes. Construtor da superclasse, é chamado antes do construtor da classe derivada.

- Lembrar de diferenciar suas relações
"Is-a" (é um): refere-se a generalização/especialização)

```Java
class Student extends Person { }
```
Estudante é uma pessoa

"Has-a" (tem-um): refere-se a agregação/composição
```Java
class Person { String name; }
```
Person possui uma string (name)

#### Exemplo de recurso de implementação: extends (classe utilizada para para indicar que herda atributos/métodos de outra classe)

```Java
class Person {
  private String name;
  public Person() {
    this.name = "to be given";
  }
  public String getName() { // objeto da classe Student terá método getName()(herdado de Person)
    return this.name;
  }
}


class Student extends Person { //Student terá atributos name (herdado de Person) e course
  private String course;
  public Student() {
    this.course = "to be chosen";
  }
}


class Main {
 public static void main(String[] args) {
   Person p = new Person();
   Student s = new Student();
   System.out.println(p.getName());
   System.out.println(s.getName()); // herança em ação!
 }
}
```

### 4. Polimorfismo
Objetos de classes diferentes podem ser tratados como objetos de classe comum.

```Java
class Figura {
  public void desenha() {
    System.out.println("Desenhando Figura");
  }
}

class Triangulo extends Figura {
  public void desenha() {
    System.out.println("Desenhando Triangulo");
  }
}

class Retangulo extends Figura {
  public void desenha() {
    System.out.println("Desenhando Retangulo");
  }
}

class Main {
  public static void main(String[] args) {
    Figura figs[] = {
      new Triangulo(),
      new Triangulo(),
      new Retangulo(),
      new Retangulo() 
    };
    for (Figura f : figs)
      f.desenha();
  }
}
```
#### Polimorfismo estático
- É determinado em tempo de compilação
- Sobrecarga (overloading), paramétrico

#### Polimorfismo dinâmico
- É determinado em tempo de execução
- Sobrescrita (overriding)
  
```Java
class Figura {
  public void desenha() {
    System.out.println("Desenhando Figura");
  }
}

class Triangulo extends Figura {
  public void desenha() {
    System.out.println("Desenhando Triangulo");
  }
}

class Retangulo extends Figura {
  public void desenha() {
    System.out.println("Desenhando Retangulo");
  }
}

class Main {
  public static void main(String[] args) {
    Figura figs[] = {
      new Triangulo(),
      new Triangulo(),
      new Retangulo(),
      new Retangulo() 
    };
    for (Figura f : figs)
      f.desenha();
  }
}
```

## Relações entre objetos
### Associação
Relacionamento entre dois ou mais objetos que estão conectados por meio de suas referências de objetos.

### Dependência
Uma classe depende da outra. Se uma mudar, a outra também terá de mudar.

### Composição
Um objeto é responsável pelos objetos contidos nele.

### Agregação
Parecido com composição, no entanto, o objeto principal não é responsável pelos objetos contidos nele.

#### Referências:
[1] Conteúdo disponibilizado pela disciplina de Paradigmas de Programação
[2] medium.com/introdução-à-programação-orientada-a-objetos-7ed68508764e
