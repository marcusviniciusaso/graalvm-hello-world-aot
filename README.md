export PATH=/Library/Java/JavaVirtualMachines/graalvm-ce-java17-22.3.0/Contents/Home/bin:$PATH
export JAVA_HOME=/Library/Java/JavaVirtualMachines/graalvm-ce-java17-22.3.0/Contents/Home

javac HelloWorld.java
java HelloWorld

native-image HelloWorld
./helloworld

time java HelloWorld
time ./helloworld