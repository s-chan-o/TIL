## JVM이란?

JVM(Java Virtual Machine)은 OS에 종속받지 않고 CPU가 JAVA를 인식, 실행할 수 있게 하는 가상 컴퓨터이다.

그렇기 때문에, JAVA는 JVM에 의해 **운영체제에 독립적** 이라는 장점을 가질 수 있게됩니다.

> 컴파일 과정

![alt text](image.png)

위의 동작처럼 Java 소스코드, 즉 원시코드(myProgram.java)는 CPU가 인식을 하지 못하므로 기계어로 컴파일을 해줘야 한다.

하지만 Java는 이 JVM이라는 가상머신을 거쳐서 OS에 도달하기 때문에 OS가 인식할 수 있는 기계어로 바로 컴파일 되는게 아니라 JVM이 인식할 수 있는 Java bytecode(myProgram.java)로 변환된다. 

```
여기서 Java compiler는 JDK를 설치하면 bin에 존재하는 java.exe 이다.(JDK에 Java compiler가 포함되어 있다는 뜻)
javac 명령어를 통해 .java를 .class로 컴파일 할 수 있다
```

변환된 bytecode는 기계어가 아니기 때문에 OS가 해석할 수 없어서 JVM을 통해 bytecode를 OS가 해석 가능한 기계어(Binary Code)로 변환한다.

JAVA 언어로 작성한 소스파일은 바로 운영체제로 가는게 아니라 JVM을 거쳐서 운영체제와 상호작용을 한다. 때문에 개발자가 소스코드를 작성하는 것에 있어서 운영체제로부터 독립적일 수 있게 된다.