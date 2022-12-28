

![alt text](https://github.com/marquesbmc/images/blob/main/1-test.jpg)

*<h1 align="right">"O seu código sempre vai ser testado!" </h1>*


## 1. Definição de Teste de Software segundo Engenharia de Software

De acordo com o Padrão de Teste de Software [ANSI/IEEE 1059](https://www.softwaretestingmaterial.com/international-software-testing-standards/), o Teste em Engenharia de Software é um processo de análise de um produto ou sistema de software para examinar um produto ou sistema de software para determinar se ele satisfaz ou deixa de satisfazer as condições estabelecidas (ou seja, defeitos). O processo de teste avalia as características dos produtos de software quanto a requisitos como requisitos ausentes, bugs ou erros para avaliar sua confiabilidade, segurança e desempenho.


## 1. O objetivo dos testes de software

Com os testes de software, você garante que certas partes do nosso software funcionem conforme o esperado. Esses **testes geralmente são executados automaticamente** por meio do sistema de compilação e, portanto, ajudam o desenvolvedor a evitar quebrar o código existente durante as atividades de desenvolvimento.

Executar testes automaticamente ajuda a identificar regressões de software introduzidas por alterações no código-fonte. Ter uma **alta cobertura de teste do seu código** permite que você continue desenvolvendo recursos sem ter que realizar muitos testes manuais.

**Você deve escrever testes de software para as partes críticas e complexas do seu aplicativo.** Se você introduzir novos recursos, um conjunto de testes sólido também o protegerá contra a regressão no código existente.

Alguns desenvolvedores acreditam que cada instrução em seu código deve ser testada, mas **em geral é seguro ignorar código trivial.** Por exemplo, normalmente é inútil escrever testes para métodos getter e setter que simplesmente atribuem valores a campos. Escrever testes para essas instruções é demorado e inútil, pois você estaria testando a máquina virtual Java. A própria JVM já possui casos de teste para isso. Se você estiver desenvolvendo aplicativos de usuário final, pode presumir que uma atribuição de campo funciona em Java.

Se você começar a desenvolver testes para uma base de código existente sem nenhum teste, **é uma boa prática começar a escrever testes para código em que a maioria dos erros ocorreu no passado**. Dessa forma, você pode se concentrar nas partes críticas do seu aplicativo.

## 2.  Terminologia de teste

O código que é testado normalmente é chamado de **_código em teste_** . Se você estiver testando um aplicativo, isso será chamado de **_aplicativo em teste_** .

Um **_dispositivo de teste_** é um estado fixo de um conjunto de objetos que são usados como linha de base para a execução de testes. Outra maneira de descrever isso é uma pré-condição de teste.

Por exemplo, um acessório de teste pode ser uma string fixa, que é usada como entrada para um método. O teste validaria se o método se comporta corretamente com essa entrada.


### 2.1. Testes unitários, de integração e de desempenho

Nos testes, você distingue entre testes unitários, de integração e testes de desempenho:

-  **_O teste de unidade_** é um pedaço de código escrito por um desenvolvedor que executa uma funcionalidade específica no código a ser testado e afirma um determinado comportamento ou estado. A porcentagem de código que é testada por testes de unidade é normalmente chamada  de **_cobertura de teste_** . Um teste de unidade tem como alvo uma pequena unidade de código, por exemplo, um método ou uma classe. As dependências externas devem ser removidas dos testes de unidade, por exemplo, substituindo a dependência por uma implementação de teste ou um objeto (simulado) criado por uma estrutura de teste. Os testes de unidade não são adequados para testar interfaces de usuário complexas ou interação de componentes. Para isso, você deve desenvolver testes de integração.
    
-   **_Um teste de integração_** visa testar o comportamento de um componente ou a integração entre um conjunto de componentes. Os testes de integração verificam se todo o sistema funciona como pretendido, reduzindo assim a necessidade de testes manuais intensivos. Esses tipos de testes permitem que você traduza suas histórias de usuários em um conjunto de testes. O teste se assemelharia a uma interação esperada do usuário com o aplicativo.
    
-   **_Os testes de desempenho_** são usados ​​para comparar componentes de software repetidamente. Sua finalidade é garantir que o código em teste seja executado com rapidez suficiente, mesmo sob alta carga.

## 2.2. Teste de comportamento vs. estado

Um teste é um teste de comportamento (também chamado teste de interação) se verifica se determinados métodos foram chamados com os parâmetros de entrada corretos. Um teste de comportamento não valida o resultado de uma chamada de método.

-   **_Teste de estado_**  é sobre validar o resultado. 

-   **_Teste de comportamento_**  é sobre testar o comportamento do aplicativo em teste.

Se você estiver testando algoritmos ou funcionalidades do sistema, na maioria dos casos você pode querer testar o estado e não as interações. **Uma configuração de teste típica usa mocks ou stubs de classes relacionadas para abstrair as interações com essas outras classes.** Depois você testa o estado ou o comportamento dependendo de sua necessidade.

## 3. Convenções de nomenclatura de classes e métodos de teste

Existem várias convenções de nomenclatura em potencial para testes de software. Uma solução amplamente usada para classes é **usar o sufixo _Test_ ou _Tests_ no final dos nomes das classes de teste.** Essa convenção também é usada pelo sistema de compilação popular para identificar o teste a ser executado.

Como regra geral, um nome de método para um nome deve explicar o que o teste faz. Se isso for feito corretamente, a leitura da implementação real pode ser evitada.

Uma convenção possível é usar o "deveria" no nome do método de teste. Por exemplo, `ordersShouldBeCreated`ou `menuShouldGetActive`. Isso dá uma dica do que deve acontecer se o método de teste for executado.

Outra abordagem é usar `given[ExplainYourInput]When[WhatIsDone]Then[ExpectedResult]`para o nome de exibição do método de teste.

## 4. Objetos simulados (Mock)

Em seus testes de unidade, você deseja testar determinada funcionalidade (a classe em teste) isoladamente. Outras funcionalidades necessárias para testar a classe em teste devem ser controladas para evitar efeitos colaterais.

Um **_objeto simulado_** é uma implementação fictícia de uma interface ou classe. Os objetos simulados permitem definir a saída de determinadas chamadas de métodos. Eles normalmente registram a interação com o sistema e os testes podem validar isso.

**Você pode criar objetos fictícios manualmente (via código)** ou usar uma estrutura fictícia para simular essas classes. As estruturas simuladas permitem que você crie objetos simulados em tempo de execução e defina seu comportamento.

O **exemplo** clássico de um objeto simulado é um provedor de dados. Na produção é usada uma implementação para conectar à fonte de dados real. Mas para testar um objeto simulado, nós simulamos a fonte de dados para garantir que as condições de teste sejam sempre as mesmas.

Esses objetos simulados podem ser fornecidos para a classe que é testada. **Portanto, a classe a ser testada deve evitar qualquer dependência de dados externos.**

As estruturas simuladas ou simuladas permitem testar a interação esperada com o objeto simulado. Você pode, por exemplo, validar que apenas determinados métodos foram chamados no **objeto mock.**


  ## 5.Teste de unidade com JUnit 4

### 5.1. A estrutura JUnit
[JUnit](http://junit.org/) é uma estrutura de teste que usa anotações para identificar métodos que especificam um teste. JUnit é um projeto de código aberto hospedado no [Github](https://github.com/junit-team/junit) .

### 5.2. A estrutura JUnitComo definir um teste no JUnit?

_Um teste_ JUnit é um método contido em uma classe que é usado apenas para teste. Isso é chamado **_de classe de teste_** . Para definir que um determinado método é um método de teste, anote-o com a `@Test`anotação.

Este método executa o código em teste. Você usa um método **_assert_** , fornecido pelo JUnit ou outra estrutura assert, para verificar um resultado esperado versus o resultado real. Essas chamadas de método são normalmente chamadas de **_asserts_** ou **_declarações assert_** .

**Você deve fornecer mensagens significativas em declarações assert.** Isso torna mais fácil para o usuário identificar e corrigir o problema. Isso é especialmente verdadeiro se alguém olhar para o problema, que não escreveu o código em teste ou o código de teste.

### 5.3. Exemplo de teste unitário

O código a seguir mostra um teste JUnit usando a versão JUnit 4.

Suponha que você tenha essa classe que deseja testar.


```
package br.gov.caixa.sixxx;

public class Calculator {

    public int multiply(int a, int b) {
        return a * b;
    }
}
```

Uma classe de teste contendo testes de software para a classe acima pode ter a seguinte aparência.


```
package br.gov.caixa.sixxx;

import static org.junit.Assert.assertEquals;

import org.junit.Before;
import org.junit.Test;

public class CalculatorTest {

    private Calculator calculator;

    @Before
    void setUp() throws Exception {
        calculator = new Calculator();
    }

    @Test
    void testMultiply() {
        assertEquals( "Regular multiplication should work", calculator.multiply(4,5), 20);
    }

    @Test
    void testMultiplyWithZero() {
        assertEquals("Multiple with zero should be zero",0,  calculator.multiply(0,5));
        assertEquals("Multiple with zero should be zero", 0, calculator.multiply(5,0));
    }
}
```
### 5.4.  Convenções de nomenclatura JUnit para Maven

Se estiver usando o sistema de compilação Maven, você deve usar o sufixo "Test" para classes de teste. O sistema de compilação Maven (por meio de seu plug-in surfire) inclui automaticamente essas classes em seu escopo de teste.

Esta classe pode ser executada como qualquer outro programa Java na linha de comando. Você só precisa adicionar o arquivo JAR da biblioteca JUnit ao caminho de classe.

## 6. Usando JUnit 4

### 6.1. Instalaçao JUnit com Maven
Para usar JUnit em sua compilação do Maven, adicione a seguinte dependência ao seu arquivo pom.
```
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```


### 6.2. Definindo métodos de teste

JUnit usa anotações para marcar métodos como métodos de teste e configurá-los. A tabela a seguir fornece uma visão geral das anotações mais importantes no JUnit para as versões 4.xe 5.x. Todas essas anotações podem ser usadas em métodos.

*Tabela 1. Anotações*

| JUnit 4 | Descrição |
|---------|-----------|
| import org.junit.* | Instrução de importação para usar as anotações a seguir. |
| @Test | Identifica um método como um método de teste. |
| @Before | Executado antes de cada teste. Ele é usado para preparar o ambiente de teste (por exemplo, ler dados de entrada, inicializar a classe). |
| @After | Executado após cada teste. Ele é usado para limpar o ambiente de teste (por exemplo, excluir dados temporários, restaurar padrões). Ele também pode economizar memória limpando estruturas de memória caras. |
| @BeforeClass | Executado uma vez, antes do início de todos os testes. Ele é usado para realizar atividades intensivas em tempo, por exemplo, para se conectar a um banco de dados. Os métodos marcados com esta anotação precisam ser definidos `static`para funcionar com JUnit. |
| @AfterClass | Executado uma vez, após a conclusão de todos os testes. Ele é usado para realizar atividades de limpeza, por exemplo, para se desconectar de um banco de dados. Os métodos anotados com esta anotação precisam ser definidos `static`para funcionar com JUnit. |
|@Test (expected = Exception.class)|Falha se o método não lançar a exceção nomeada.|
|@Test(timeout=100)|Falha se o método demorar mais de 100 milissegundos.|
------------------------------------------------------------------------------

### 6.3. Declarações de declaração

JUnit fornece métodos estáticos para testar determinadas condições por meio da `Assert`classe. Essas **_declarações assert_** geralmente começam com `assert`. Eles permitem que você especifique a mensagem de erro, o resultado esperado e o resultado real. Um _método de asserção_ compara o valor real retornado por um teste com o valor esperado. Ele lança um `AssertionException`se a comparação falhar.

A tabela a seguir fornece uma visão geral desses métodos. Os parâmetros entre colchetes [] são opcionais e do tipo String.


*Tabela 2. Métodos para afirmar os resultados do teste*

| Declaração | Descrição |
|--|--|
| falha([mensagem]) | Deixe o método falhar. Pode ser usado para verificar se uma determinada parte do código não foi alcançada ou para ter um teste com falha antes que o código de teste seja implementado. O parâmetro mensagem é opcional. |
| assertTrue([mensagem,] condição booleana) | Verifica se a condição booleana é verdadeira. |
| assertFalse([mensagem,] condição booleana) | Verifica se a condição booleana é falsa. |
| assertEquals([mensagem,] esperado, real) | Testa se dois valores são iguais. Nota: para arrays a referência é verificada e não o conteúdo dos arrays. |
| assertEquals([mensagem,] esperado, real, tolerância) | Teste se os valores float ou double correspondem. A tolerância é o número de casas decimais que devem ser iguais. |
| assertNull([mensagem,] objeto) | Verifica se o objeto é nulo. |
| assertNotNull([mensagem,] objeto) | Verifica se o objeto não é nulo. |
| assertSame([mensagem,] esperado, real) | Verifica se ambas as variáveis ​​se referem ao mesmo objeto. |
| assertNotSame([mensagem,] esperado, real) | Verifica se ambas as variáveis ​​se referem a objetos diferentes. |


### 6.4  Conceito de suítes de teste JUnit

Se você tiver várias classes de teste, poderá combiná-las em um conjunto de testes. A execução de um conjunto de testes executa todas as classes de teste desse conjunto na ordem especificada. Um conjunto de testes também pode conter outros conjuntos de testes.

O código de exemplo a seguir demonstra o uso de um conjunto de testes. Ele contém duas classes de teste (MyClassTest e MySecondClassTest). Se você quiser adicionar outra classe de teste, poderá adicioná-la à `@Suite.SuiteClasses`instrução.

```
package br.gov.caixa.sixxx;

import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({
        MyClassTest.class,
        MySecondClassTest.class })

public class AllTests {

}
```
### 6.5  Desativando testes

A anotação @Ignore permite ignorar estaticamente um teste. Alternativamente, você pode usar `Assume.assumeFalse`ou `Assume.assumeTrue`para definir uma condição para o teste. `Assume.assumeFalse`marca o teste como inválido, se sua condição for avaliada como verdadeira. `Assume.assumeTrue`avalia o teste como inválido se sua condição for avaliada como falsa. Por exemplo, o seguinte desabilita um teste no Linux:

```
Assume.assumeFalse(System.getProperty("os.name").contains("Linux"));
```

### 6.6  Teste parametrizado

JUnit permite que você use parâmetros em uma classe de testes. Esta classe pode conter **um** método de teste e este método é executado com os diferentes parâmetros fornecidos.

Você marca uma classe de teste como um teste parametrizado com a `@RunWith(Parameterized.class)`anotação.

Essa classe de teste deve conter um método estático anotado com a `@Parameters`anotação. Esse método gera e retorna uma coleção de arrays. Cada item desta coleção é usado como parâmetro para o método de teste.

Você pode usar a `@Parameter`anotação em campos públicos para obter os valores de teste injetados no teste.

O código a seguir mostra um exemplo para um teste parametrizado. Ele testa o `multiply()`método da `MyClass`classe que está incluída como classe interna para o propósito deste exemplo.

```
package br.gov.caixa.sixxx.testing;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

import java.util.Arrays;
import java.util.Collection;

import static org.junit.Assert.assertEquals;
import static org.junit.runners.Parameterized.*;

@RunWith(Parameterized.class)
public class ParameterizedTestFields {

    // fields used together with @Parameter must be public
    @Parameter(0)
    public int m1;
    @Parameter(1)
    public int m2;
    @Parameter(2)
    public int result;


    // creates the test data
    @Parameters
    public static Collection<Object[]> data() {
        Object[][] data = new Object[][] { { 1 , 2, 2 }, { 5, 3, 15 }, { 121, 4, 484 } };
        return Arrays.asList(data);
    }


    @Test
    public void testMultiplyException() {
        MyClass tester = new MyClass();
        assertEquals("Result", result, tester.multiply(m1, m2));
    }


    // class to be tested
    class MyClass {
        public int multiply(int i, int j) {
            return i *j;
        }
    }

}
```

Como alternativa ao uso da `@Parameter`anotação, você pode usar um construtor no qual armazena os valores de cada teste. O número de elementos em cada array fornecido pelo método anotado `@Parameters` deve corresponder ao número de parâmetros no construtor da classe. A classe é criada para cada parâmetro e os valores de teste são passados ​​por meio do construtor para a classe.

.

```
package br.gov.caixa.sixxx.testing.junit.first;

import static org.junit.Assert.assertEquals;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

@RunWith(Parameterized.class)
public class ParameterizedTestUsingConstructor {

    private int m1;
    private int m2;

    public ParameterizedTestUsingConstructor(int p1, int p2) {
        m1 = p1;
        m2 = p2;
    }

    // creates the test data
    @Parameters
    public static Collection<Object[]> data() {
        Object[][] data = new Object[][] { { 1 , 2 }, { 5, 3 }, { 121, 4 } };
        return Arrays.asList(data);
    }


    @Test
    public void testMultiplyException() {
        MyClass tester = new MyClass();
        assertEquals("Result", m1 * m2, tester.multiply(m1, m2));
    }


    // class to be tested
    class MyClass {
        public int multiply(int i, int j) {
            return i *j;
        }
    }

}
```
Se você executar esta classe de teste, o método de teste será executado com cada parâmetro definido. No exemplo acima, o método de teste é executado três vezes.

Uma abordagem mais flexível e fácil de escrever é fornecida pelo JUnitParams de [https://github.com/Pragmatists/JUnitParams](https://github.com/Pragmatists/JUnitParams) .

### 6.7. Regras JUnit

Por meio de regras JUnit, você pode adicionar comportamento a cada teste em uma classe de teste. Você pode anotar campos do tipo `TestRule`com a `@Rule`anotação. Você pode criar objetos que podem ser usados ​​e configurados em seus métodos de teste. Isso adiciona mais flexibilidade aos seus testes. Você pode, por exemplo, especificar qual mensagem de exceção você espera durante a execução do seu código de teste.

```
package br.gov.caixa.sixxx.testing.junit.first;

import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;

public class RuleExceptionTesterExample {

  @Rule
  public ExpectedException exception = ExpectedException.none();

  @Test
  public void throwsIllegalArgumentExceptionIfIconIsNull() {
    exception.expect(IllegalArgumentException.class);
    exception.expectMessage("Negative value not allowed");
    ClassToBeTested t = new ClassToBeTested();
    t.methodToBeTest(-1);
  }
}
```

JUnit já fornece várias implementações de regras úteis. Por exemplo, a `TemporaryFolder`classe permite configurar arquivos e pastas que são removidos automaticamente após cada execução de teste.

O código a seguir mostra um exemplo para o uso da `TemporaryFolder`implementação.

```
package br.gov.caixa.sixxx.testing.junit.first;

import static org.junit.Assert.assertTrue;

import java.io.File;
import java.io.IOException;

import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.TemporaryFolder;

public class RuleTester {

  @Rule
  public TemporaryFolder folder = new TemporaryFolder();

  @Test
  public void testUsingTempFolder() throws IOException {
    File createdFolder = folder.newFolder("newfolder");
    File createdFile = folder.newFile("myfilefile.txt");
    assertTrue(createdFile.exists());
  }
}
```

Para obter mais exemplos de regras existentes, consulte [https://github.com/junit-team/junit4/wiki/Rules](https://github.com/junit-team/junit4/wiki/Rules) .

### 6.8. Escrevendo regras JUnit personalizadas

Para escrever sua regra personalizada, você precisa implementar a `TestRule`interface. Esta interface define o `apply(Statement, Description)`método que deve retornar uma instância de `Statement`. A instrução representa os testes dentro do tempo de execução do JUnit e Statement#evaluate() os executa. Descrição descreve o teste individual. Permite ler informações sobre o teste via reflexão.

Veja a seguir um exemplo simples para adicionar uma instrução de log a um aplicativo Android antes e depois da execução do teste.

```
package br.gov.caixa.sixxx.testing.junit.asynctask;

import android.util.Log;

import org.junit.rules.TestRule;
import org.junit.runner.Description;
import org.junit.runners.model.Statement;

public class MyCustomRule implements TestRule {
    private Statement base;
    private Description description;

    @Override
    public Statement apply(Statement base, Description description) {
        this.base = base;
        this.description = description;
        return new MyStatement(base);
    }

    public class MyStatement extends Statement {
        private final Statement base;

        public MyStatement(Statement base) {
            this.base = base;
        }

        @Override
        public void evaluate() throws Throwable {
            System.
            Log.w("MyCustomRule",description.getMethodName() + "Started" );
            try {
                base.evaluate();
            } finally {
                Log.w("MyCustomRule",description.getMethodName() + "Finished");
            }
        }
    }
}
```

Para usar essa regra, basta adicionar um campo anotado `@Rule`à sua classe de teste.

```
@Rule
public MyCustomRule myRule = new MyCustomRule();
```

### 6.9. Categorias 

É possível definir categorias de testes e incluí-los ou excluí-los com base em anotações. O exemplo a seguir é baseado nas [notas de versão do JUnit 4.8](https://github.com/junit-team/junit/blob/master/doc/ReleaseNotes4.8.md) .

```
public interface FastTests { /* category marker */
}

public interface SlowTests { /* category marker */
}

public class A {
    @Test
    public void a() {
        fail();
    }

    @Category(SlowTests.class)
    @Test
    public void b() {
    }
}

@Category({ SlowTests.class, FastTests.class })
public class B {
    @Test
    public void c() {
    }
}

@RunWith(Categories.class)
@IncludeCategory(SlowTests.class)
@SuiteClasses({ A.class, B.class })
// Note that Categories is a kind of Suite
public class SlowTestSuite {
    // Will run A.b and B.c, but not A.a
}

@RunWith(Categories.class)
@IncludeCategory(SlowTests.class)
@ExcludeCategory(FastTests.class)
@SuiteClasses({ A.class, B.class })
// Note that Categories is a kind of Suite
public class SlowTestSuite {
    // Will run A.b, but not A.a or B.c
}
```

### 6.10. Importações estáticas JUnit

A importação estática é um recurso que permite que campos e métodos definidos em uma classe `public static`sejam usados ​​sem especificar a classe na qual o campo está definido.

As instruções de assert JUnit são normalmente definidas `public static`para permitir que o desenvolvedor escreva instruções de teste curtas. O trecho a seguir demonstra uma instrução assert com e sem importações estáticas.
.

```
// without static imports you have to write the following statement
Assert.assertEquals("10 x 5 must be 50", 50, tester.multiply(10, 5));


// alternatively define assertEquals as static import
import static org.junit.Assert.assertEquals;

// more code

// use assertEquals directly because of the static import
assertEquals("10 x 5 must be 50", 50, tester.multiply(10, 5));
```
