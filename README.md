## **Randoop**

Parece ser realmente um gerador de entradas como esperamos. O foco parece ser em teste unitário, porém o uso ainda está sendo totalmente via linha de comando.

```jsx
java -Xmx3000m -classpath /Users/thiagofernandes/development/test_randoop/:${RANDOOP_JAR} randoop.main.Main gentests --testclass=Trivialissimo --output-limit=100
```

Com o comando acima, pedi para ser gerado 100 testes unitários para o método de soma. Foram gerados diversos cenários, mas para isso foram gerados inúmeros métodos e não uma forma mais otimizada de fazer testes parametrizados. Além disso, o uso de linha de comando acaba por tornar um processo muito mais artesanal do que o que poderia ser feito através de um plugin direto na IDE com as gerações das classes de testes no pacote adequado.

Apesar disso, os cenários gerados foram relevantes e cobriram diferentes possibilidades, por exemplo o uso de números negativos:

```java

```

tentativa de fazer soma com letra:

```java
public void test07() throws Throwable {
    if (debug)
        System.out.format("%n%s%n", "RegressionTest0.test07");
    int int2 = Trivialissimo.soma(0, (int) 'a');
    org.junit.Assert.assertTrue("'" + int2 + "' != '" + 97 + "'", int2 == 97);
}
```

No caso do método de divisão, tentou dividir por zero:

```java
@Test
public void test13() throws Throwable {
    if (debug)
        System.out.format("%n%s%n", "RegressionTest0.test13");
    // The following exception was thrown during execution in test generation
    try {
        int int2 = Trivialissimo.divisao((int) (short) 1, (int) (short) 0);
        org.junit.Assert.fail("Expected exception of type java.lang.ArithmeticException; message: / by zero");
    } catch (java.lang.ArithmeticException e) {
        // Expected exception.
    }
}
```

Dividir por número negativo:

```java
@Test
public void test14() throws Throwable {
    if (debug)
        System.out.format("%n%s%n", "RegressionTest0.test14");
    int int2 = Trivialissimo.divisao((int) 'a', (-1));
    org.junit.Assert.assertTrue("'" + int2 + "' != '" + (-97) + "'", int2 == (-97));
}
```