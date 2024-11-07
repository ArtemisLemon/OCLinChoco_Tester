# OCLinChoco Tester

Essentially a App.java class with a main funtion, to test [OCLinChoco](https://github.com/ArtemisLemon/OCLinChoco)

## How to Include OCLinChoco
You can follow this simple project structure to add OCLinChoco and Choco to your Gradle App

### Starting your OCLinChoco project
```bash
gradle init
git init
git add submodule \<URL\> OCLinChoco
```

### Configuring Gradle
See `settings.gradle` and `app/build.gradle`, essentially add:
```groovy
//settings.gradle
include('OCLinChoco:lib')
project(':OCLinChoco:lib').projectDir = new File(rootDir, 'OCLinChoco/lib')
```

```groovy
//app/build.gradle
dependencies {
    implementation project(':OCLinChoco:lib') //also exposes Choco-Solver API
}
```

### Make an OCL CSP to Solve
in app/src/main/java/org/example/App.java
```java
package org.example;
import org.oclinchoco.ReferenceTable;
import org.chocosolver.solver.Model; //exposed API

public class App {
    public static void main(String[] args) {

        int numA = 10; int cardA2B=3;
        int numB = 23; int cardB2A=1;

        Model csp = new Model();

        ReferenceTable a2b = new ReferenceTable(csp,numA,cardA2B,numB);
        ReferenceTable b2a = new ReferenceTable(csp,numB,cardB2A,numA);
    }
}
```