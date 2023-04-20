# Teste de compilação ahead-of-time da GraalVM

## O que é GraalVM?

GraalVM é uma JDK de alto desempenho que pode, além de melhorar o desempenho, diminuir o consumo de recursos de aplicações Java e outras linguagems que rodam na JVM. (Quarkus)[https://quarkus.io/] utiliza recursos da GraalVM para criar aplicações nativas de alto desempenho.

## Compilação just-in-time

Na compilação just-in-time a aplicação Java é compilada para bytecode. É possível rodar esse bytecode em qualquer plataforma com JVM. Porém, quando o usuário acessa, a aplicação passa por uma segunda compilação para o código de máquina. Dessa forma, há um processamento adicional para interpretar o bytecode para a plataforma atual. É a compilação padrão da JDK.

Nesse tipo de compilação há menos tempo de compilação, porém mais tempo de execução
-Tempo de compilação
+Tempo de execução

![just-in-time](/resources/img/just-in-time.png "just-in-time")

## Compilação ahead-of-time

Na compilação ahead-of-time a aplicação Java é compilada para bytecode e logo em seguida é compilada para o código de máquina da plataforma atual. A imagem nativa criada pode ser executada somente na plataforma para a qual ela foi criada. Tudo que a aplicação precisa é empacotado dentro do executável.

Nesse tipo de compilação há mais tempo de compilação, porém menos tempo de execução.
+Tempo de compilação
-Tempo de execução

![ahead-of-time](/resources/img/ahead-of-time.png "ahead-of-time")

export PATH=/Library/Java/JavaVirtualMachines/graalvm-ce-java17-22.3.0/Contents/Home/bin:$PATH
export JAVA_HOME=/Library/Java/JavaVirtualMachines/graalvm-ce-java17-22.3.0/Contents/Home

javac HelloWorld.java
java HelloWorld

native-image HelloWorld
./helloworld

time java HelloWorld
time ./helloworld