# Teste de compilação ahead-of-time da GraalVM

## O que é GraalVM?

GraalVM é uma JDK de alto desempenho que pode, além de melhorar o desempenho, diminuir o consumo de recursos de aplicações Java e outras linguagems que rodam na JVM. [Quarkus](https://quarkus.io/) utiliza recursos da GraalVM para criar aplicações nativas de alto desempenho.

## Compilação just-in-time (JIT)
Na compilação just-in-time a aplicação Java é compilada para bytecode. É possível rodar esse bytecode em qualquer plataforma com JVM. Porém, quando o usuário acessa, a aplicação passa por uma segunda compilação para o código de máquina. Dessa forma, há um processamento adicional para interpretar o bytecode para a plataforma atual. É a compilação padrão da JDK.

Nesse tipo de compilação há menos tempo de compilação, porém mais tempo de execução  
-Tempo de compilação  
+Tempo de execução

![just-in-time](/resources/img/just-in-time.png "just-in-time")

## Compilação ahead-of-time (AOT)

Na compilação ahead-of-time a aplicação Java é compilada para bytecode e logo em seguida é compilada para o código de máquina da plataforma atual. A imagem nativa criada pode ser executada somente na plataforma para a qual ela foi criada. Tudo que a aplicação precisa é empacotado dentro do executável.

Nesse tipo de compilação há mais tempo de compilação, porém menos tempo de execução.  
+Tempo de compilação  
-Tempo de execução

![ahead-of-time](/resources/img/ahead-of-time.png "ahead-of-time")

## Instalar GraalVM

A instalação da GraalVM pode ser feita seguindo o [guia para intalação](https://www.graalvm.org/22.3/docs/getting-started/#install-graalvm) de cada plataforma.

Após instalar, é necessário configurar as variáveis de ambiente Java.

```bash
export PATH=/Library/Java/JavaVirtualMachines/graalvm-ce-java17-22.3.0/Contents/Home/bin:$PATH
export JAVA_HOME=/Library/Java/JavaVirtualMachines/graalvm-ce-java17-22.3.0/Contents/Home
```

Para verificar a versão da GraalVM instalada:
![java-version](/resources/img/java-version.png "Versão do Java")

## Teste

Compilar para bytecode:
```bash
javac HelloWorld.java
```

Executar classe:
```bash
java HelloWorld
```
![execute-class](/resources/img/execute-class.png "Executar classe")

Até agora utilizamos somente a compilação just-in-time. Para utilizar a compilação ahead-of-time é necessária criar uma imagem nativa com o utilitário [native-image](https://www.graalvm.org/22.3/reference-manual/native-image/#install-native-image) a partir da classe:
```bash
native-image HelloWorld
```
![native-image](/resources/img/native-image.png "Imagem nativa")

O bytecode é transformado em um executável com código de máquina. Para executar:
```bash
./helloworld
```
![execute-native-image](/resources/img/execute-native-image.png "Executar imagem nativa")

É possível comparar o tempo de execução com o comando time:
```bash
time java HelloWorld
time ./helloworld
```
![execution-time](/resources/img/execution-time.png "Tempo de execução")

As duas primeiras execuções são com a aplicação compilada em JIT e as duas últimas são com a aplicação compilada em AOT.  
Melhor tempo com JIT: 0,078  
Melhor tempo com AOT: 0,013