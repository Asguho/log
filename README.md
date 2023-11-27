
# Pass by value vs. pass by reference

### 18-08-2023

**Pass by value** og **pass by reference** refererer til, hvordan argumenter bliver overført til funktioner eller metoder i et programmeringssprog.

### Pass by value

I Java anvendes **pass by value**. Dette betyder, at når du sender en værdi som et argument til en funktion eller metode, sender du faktisk en kopi af værdien, og ændringer foretaget inden for funktionen påvirker ikke den originale værdi udenfor funktionen. Dette gælder for primitive datatyper som int, float, char osv.

### Pass by reference

På den anden side, i **pass by reference**, ville ændringer foretaget inden for funktionen påvirke den oprindelige værdi udenfor funktionen. Dette er mere typisk for sprog som C++ med referencer eller pointers, hvor du kan manipulere selve hukommelsesadressen.

### Objekter i java

I Java er det dog vigtigt at bemærke, at selvom objekter overføres ved hjælp af pass by value, overføres værdien af objektreferencen, ikke selve objektet. Dette betyder, at når du sender en objektreference som argument, kan du stadig ændre tilstanden af det objekt, som referencen peger på, men du kan ikke ændre selve referencen, så den peger på et andet objekt. Dette kan undertiden føre til forvirring, da det ikke er helt det samme som traditionel pass by reference.

https://sentry.io/answers/java-pass-by-reference-or-value/

# String object in Java

Når vi taler om streng objekter i Java, er de **immutable**. Dette betyder, at de ikke kan ændres efter at være blevet oprettet. Når du foretager ændringer på en streng, såsom at tilføje, fjerne eller ændre tegn, oprettes der faktisk en helt ny streng. Den oprindelige streng forbliver uændret i hukommelsen. Dette designvalg har flere fordele, da Java nu kan pege på den samme sted i streng i memory for alle ens strenge. Når en ny streng oprettes, søger Java Virtual Machine (JVM) i det område, den har allokeret til Java String Pool, og hvis den finder strengen der, returnerer den blot hukommelsesreferencen.

Her er et eksempel:

```java
String constantString1 = "Hello world";
String constantString2 = "Hello world";
assertThat(constantString1).isSameAs(constantString2);
```


*I det tidligere eksempel opretter vi to strenge og tester, om de har en reference til det samme sted i memory*

Dette designvalg har både fordele og ulemper. Det letter skrivningen af flertrådet kode og giver mulighed for nogle optimeringer. Dog kan det blive dyrt at ændre værdien af en streng. Hvis der er behov for mange ændringer, bør man overveje at bruge `StringBuilder` eller `StringBuffer`. Disse klasser tillader mere effektive ændringer i strengen.

**@Anders Jeg har lidt svært ved at se, hvorfor dette design valg er blevet taget. Personligt ville jeg tænke at de fleste der ikke har læst op på det, og derfor ville de  ikke bruge en `StringBuilder`, og stadig ændre på strengen, hvilket hvis jeg har forstået det rigtigt ville gøre programmet signifikant langsommere. 
Hvis man ville have at strengen var immutable, så kunne man jo bare ændre den til en konstant. Er der noget jeg overser?**

(Du mere end velkommen til at lave en pull request og erstatte denne parantese med svaret, det kunne være lidt sejt, ellers kan vi også bare tage den mundligt næste gang. Tak på forhånd)

https://www.baeldung.com/java-string-pool

# Modulus
Modulus operationen, ofte kaldet "modulo", handler om at finde resten, når et tal deles med et andet tal. Det bruges ofte med symbolet "%". For eksempel er 10 % 3 lig med 1, fordi når 10 deles med 3, er resten 1.
## Eksempel
### Kode
```java
void setup(){
  clear();
  size(500,500);
}

void draw(){
  noStroke();
  fill(0,3);
  rect(0,0,500,500);
  fill(255);
  rect(frameCount % width,(height/6)*1, 2,2);
  rect(frameCount % width,(frameCount % (width/10)) + (height/6)*2, 2,2);
  rect(frameCount % width,(frameCount/50 % 2)*30 + (height/6)*3, 2,2);
  rect(frameCount % width,(height/6)*4, 2,frameCount % (height/10));
  fill(frameCount/2 % 255, 100, 0);
  rect(frameCount % width,(height/6)*5, 2,2);
}
```
### Resultat
![](Pasted%20image%2020230819130047.png)
# kompas
### If statement
En if-erklæring er en betinget udførelsesstruktur i programmering, der bruges til at vælge mellem to forskellige handlinger baseret på en betingelse. Hvis betingelsen er sand, udføres koden inde i if-blokken.

### Switch case
Switch-case er en anden type betinget udførelsesstruktur, der bruges i programmering. Det bruges til at vælge en handling blandt flere muligheder baseret på værdien af en variabel eller en udtryk.
### kode
```java
void setup() {
    fullScreen();
}

void draw() {
    background(255);
    /*
     I calculate the angle of the vector from the middel to the mouse position. We get the angel in radians, so we divide by PI and plus by 1 and multiply by 2 to get a value between -2 and 2. We then round the value to the nearest integer, and pass it as the switch argument.
     */
   switch(round((new PVector(mouseX - width / 2, mouseY - height / 2).heading() / PI) * 2)) {
        case -2 :
        case 2 :
            printInCenter('W');
        break;  
        case 1 :
            printInCenter('S');
        break;
        case 0 :
            printInCenter('E');
        break;
        case -1 :
            printInCenter('N');
        break;
    }
}
  
void printInCenter(char s) {
    textSize(128);
    fill(0);
    textAlign(CENTER, CENTER);
    text(s, width / 2, height / 2);
}
```
### Resultat
![](Pasted%20image%2020230823124320.png)

# Loops - for og while
## Miniopgaver
```java
void setup() {
    size(500, 500);
    opg1();
    opg2();
    opg3();
    opg4();
    opg5();
    opg6();
    opg9(); // har sat 9 her, da der ser bedst ud
    opg7();
    opg8();
    opg10();
}

void opg1() {
    println("opg 1");
    for (int i = 0; i <= 10; i++) {
        println("i: "+i);
    }

    int i = 0;
    while(i<=10){
        println("i: "+i);
        i++;
    }
}

void opg2() {
    println("opg 2");
    for (int i = 0; i < 10; i+=2) {
            println("i: "+i);
    }

    int i = 0;
    while(i<10){
        println("i: "+i);
        i+=2;
    }
}
void opg3(){
    println("opg 3");
    int sum = 0;
    for (int i = 0; i < 100; i++) {
        sum += i;
    }
    println("sum: "+sum);

    sum = 0;
    int i = 0;
    while(i < 100){
        sum += i;
        i++;
    }
    println("sum: "+sum);
}

void opg4(){
    println("opg 4");
    for (int i = 10; i != 0; i--) {
        println("i: "+i);

    }
    println("while loop");
    int i = 10;
    while(i!=0){
        println("i: "+i);
        i--;
    }
}

// fra nu af laver jeg kun for loops, da det mest er "syntaktisk sukker"

void opg5(){
    println("opg 5");
    for (int i = 5; i <= 50; i+=5) {
        println("i: "+i);
    }
}

void opg6(){
    println("opg 6");
    for (int i = 1; i <= 5; i++) {
        println("i: "+pow(2,i));
    }
}

void opg7(){
    println("opg 7");
    stroke(0);
    for(int x = 0; x < width; x+=10){
        line(x,0,x,height);
    }
}

void opg8(){
    println("opg 8");
    stroke(255);
    float distance = 0;
    for (float angle = 0; angle < 360*100; angle += .1) {
        float x = width/2 + cos(radians(angle))*distance;
        float y = height/2 + sin(radians(angle))*distance;
        point(x,y);
        distance += .01;
    }
}

void opg9(){
    println("opg 9");
    for (int i = 0; i < height; i++) {
        colorMode(HSB, 255, 100, 100);
        stroke(round((float(i)/float(height))*255), 100, 100);
        line(0,i,width,i);
    }
}

void opg10(){
    println("opg 10");
    int width = 10;
    int x = 0;
    for (int i = 0; i < 10; i++) {
        rect(x, height-i*10, width, 5);
        x+=width;
        rect(x, height-i*10+5, 5, -10);
        width+=10;
    }
}
```
### Resultat
![](Pasted%20image%2020230905221017.png)
## for-firkant
```java
void ekstraOpgave(){
    //lav 10x10 små firkanter i midten af skærmen hvor firkanterne bliver gradvist mere røde nedad og gradvist mere grønne mod højre
    println("ekstra opgave");
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 10; j++) {
            colorMode(RGB, 255, 255, 255);
            noStroke();
            fill(j*25, i*25, 0);
            rect(width/10*i, height/10*j, width/10, height/10);
        }
    }
}
```
### Resultat
![](Pasted%20image%2020230905220949.png)
# Nested for-loops
## Tegn cirkler
### Kode
```java
void setup(){
    size(500, 500);
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 10; j++) {
            circle(width/10*i+20, height/10*j+20, width/20);
        }
    }
}
```
### Resultat
![](Pasted%20image%2020230906112025.png)

## Skakbræt ekstra svær
### Kode
``` java
void setup(){
    size(500, 500);
    for (int i = 0; i < 10*10; i++) {
        fill((i+(width/10*i)/width)%2*255);
        square((width/10*i)%width, ((width/10*i)/width)*width/10, width/10);
    }
}
```

### Resultat
![](Pasted%20image%2020230906125422.png)
## Tegn en trappe
### kode
``` java
void setup() {
    size(500, 500);
    for (int i = 0; i < 50; ++i) {
        for (int j = 0; j < i; ++j) {
            fill(i/50.0*255);
            rect(j*10, i*10, 10, 10);
        }
    }
}
```
### Resultat
![](Pasted%20image%2020230906130720.png)

# Arrays
## Miniopgaver
```java
void setup() {
    {    
        //Opret et array af heltal med 5 elementer og tildel det værdierne 1, 2, 3, 4 og 5. Udskriv arrayet.
        int[] listeHeltal = {1,2,3,4,5};
        for (int tal : listeHeltal) {
            println(tal);
        }
    }
    {
        //Lav et array af strenge, der indeholder navnene på dine yndlingsfarver. Udskriv alle farverne i arrayet.
        String[] yndlingsfarver = {"rød", "blå", "grøn", "gul", "lilla"};
        for (String farve : yndlingsfarver) {
            println(farve);
        }
    }
    {    
        //Lav et array af strenge, der indeholder navnene på dine yndlingsfarver. Udskriv alle farverne i arrayet.
        float[] temperaturer = {10.2, 15.3, 20.5, 25.9, 30.6};
        float sum = 0;
        for (float temp : temperaturer) {
            sum += temp;
        }
        println("Gennemsnitstemperaturen er " + sum/temperaturer.length);
    }
    {
        //Lav et array af boolean-værdier, der repræsenterer tilstanden af ​​10 lamper (tændt/slukket). Skriv en løkke, der tænder alle lamperne. (prøv at se om du kan gøre det grafisk)
        boolean[] lamper = new boolean[10];
        for (int i = 0; i < lamper.length; i++) {
            lamper[i] = true;
        }
        for (boolean lampe : lamper) {
            println(lampe);
        }
    }
    {
        //Byt om på det første og sidste element i et array. (uanset indhold)
        int[] listeHeltal = {1,2,3,4,5};
        int temp = listeHeltal[0];
        listeHeltal[0] = listeHeltal[listeHeltal.length-1];
        listeHeltal[listeHeltal.length-1] = temp;
        for (int tal : listeHeltal) {
            println(tal);
        }
    }
    {
        //Opret et array af strenge med navnene på forskellige frugter. Brug en for-løkke til at finde og udskrive indekset (positionen) for den første forekomst af “æble” i arrayet.
        String[] frugter = { "pære", "banan", "æble", "kiwi", "æble"};
        for (int i = 0; i < frugter.length; i++) {
            if (frugter[i].equals("æble")) {
                println("Første forekomst af æble er på position " + i);
                break;
            }
        }
    }
    {
        //Opret et array af strenge med navnene på månederne i den korrekte rækkefølge (januar, februar, marts, osv.). Skriv en for-løkke, der bytter om på rækkefølgen, så arrayet nu indeholder månederne i omvendt rækkefølge (december, november, oktober, osv.).
        String[] måneder = { "januar", "februar", "marts", "april", "maj", "juni", "juli", "august",
            "september", "oktober", "november", "december"};
        for (int i = 0; i < måneder.length/2; i++) {
            String temp = måneder[i];
            måneder[i] = måneder[måneder.length-1-i];
            måneder[måneder.length-1-i] = temp;
        }
        for (String måned : måneder) {
            println(måned);
        }
    }
}
```

# Flerdimensionelle arrays

```java
void setup(){
    // Opret en 3x3 matrix og find værdien i midten (anden række, anden kolonne).
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};
        println(matrix[1][1]);
    }
    // Opret en 2D matrix med 3 rækker og 4 kolonner, fyld den med tilfældige tal og beregn summen af hver række. Udskriv resultaterne.
    {
        int[][] matrix = new int[3][4];
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                matrix[i][j] = (int) random(10);
            }
        }

        for (int i = 0; i < matrix.length; i++) {
            int sum = 0;    
            for (int j = 0; j < matrix[i].length; j++) {
                sum += matrix[i][j];
            }
            println(sum);
        }
    }
    // Opret en 2D matrix, og transponer den, dvs. skift rækker og kolonner. Udskriv både den oprindelige og transponerede matrix

    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};

        int[][] transposedMatrix = new int[matrix.length][matrix[0].length];

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length ; j++) {
                transposedMatrix[j][i] = matrix[i][j];
            }
        }

        for (int i = 0; i < matrix.length; i++) {
            println(matrix[i]);
        }
        println();
        for (int i = 0; i < transposedMatrix.length; i++) {
            println(transposedMatrix[i]);
        }
    }
    // Opret to 2D matricer og find en metode der kan sammenligne om de har ens indhold
    {
        int[][] matrix1 = {{1,2,3},{4,5,6},{7,8,9}};
        int[][] matrix2 = {{1,2,3},{4,5,6},{7,8,9}};

        boolean equal = true;

        if (matrix1.length == matrix2.length) {
            for (int i = 0; i < matrix1.length; i++) {
                if (matrix1[i].length == matrix2[i].length) {
                    for (int j = 0; j < matrix1[i].length; j++) {
                        if (matrix1[i][j] != matrix2[i][j]) {
                            equal = false;
                        }
                    }
                } else {
                    equal = false;
                }
            }
        } else {
            equal = false;
        }

        println(equal);
    }
    // Skriv program der kan multiplicere to matricer
    {
        int[][] matrix1 = {{1,2,3},{4,5,6},{7,8,9}};
        int[][] matrix2 = {{1,2,3},{4,5,6},{7,8,9}};

        int[][] result = new int[matrix1.length][matrix2[0].length];

        for (int i = 0; i < matrix1.length; i++) {
            for (int j = 0; j < matrix2[0].length; j++) {
                for (int k = 0; k < matrix1[0].length; k++) {
                    result[i][j] += matrix1[i][k] * matrix2[k][j];
                }
            }
        }

        for (int i = 0; i < result.length; i++) {
            println(result[i]);
        }
    }
}
```

# Referencebaserede og værdibaserede datatyper

```java
void setup() {
    // Arbejde med Primitiver: Opret to variabler af typen int og tildel dem samme værdi. Prøv at ændre værdien af den ene variabel og se, hvordan det påvirker den anden.
    {
        int a = 1;
        int b = a;
        a = 2;
        println(b);
    }
    // Arbejde med Primitiv Arrays: Opret et primitivt array, f.eks. int[], og tildel det til en anden reference. Prøv at ændre værdierne i det originale array og se, om det påvirker den anden reference.
    {
        int[] a = {1, 2, 3};
        int[] b = a;
        a[0] = 4;
        println(b[0]);
    }
    // Arbejde med Arrays: Opret et array af strenge og tildel det til en anden reference. Fjern eller tilføj elementer til det originale array og se, hvordan det påvirker den anden reference.
    {
        String[] a = {"a", "b", "c"};
        String[] b = a;
        a[0] = "d";
        println(b[0]);
    }
}


```
# Opgaver i funktioner
**Hvad bruges krølle-parenteser til i en funktion (og hvad bruges krølle-parenteser til generelt…)**

Til at definerer scope

**Hvad anvendes almindelige parenteser til i en funktion**

Til at definere parametre

**Hvad betyder “returtype” og hvor skrives den i en funktion**

Returtypen er den type værdi funktionen returnere, og den skrives før funktionsnavnet

**Hvad er forskellen på argumenter og parametre**

parametre er dem man definerer i funktions-deklarationen og argumenter er det man sender til funktionen, når man kalder den

**Hvornår er det smart at bruge funktioner**

Når man skal bruge samme kode flere gange

**Hvad betyder “return” og hvordan anvendes det**

At funktionen returnere en værdi, og det anvendes til at returnere en værdi

**Hvad betyder “void” og hvordan anvendes det**

At funktionen ikke returnere en værdi, og det anvendes til at definere at funktionen ikke returnere en værdi

**Lav en funktion med navnet “udskriv10”, der kan udskrive 10-tabellen.**
```java
void udskriv10(){
    for (int i = 1; i <= 10; i++) {
        println(i*10);
    }
}
```
**Lav en funktion med navnet “gangMed10”, der modtager et tal som parameter og returnere tallet multipliceret med 10**
```java
int gangMed10(int tal){
    return tal*10;
}
```
**Lav en funktion med navnet “udskrivTabel”, der modtager et tal og udskriver de første 10 tal af den tabel, der svarer til inputtet**
```java
void udskrivTabel(int tal){
    for (int i = 1; i <= 10; i++) {
        println(i*tal);
    }
}
```
**Lav en funktion “mult”, der modtager to tal som parametre, og returnere resultatet som er de to tal ganget sammen**
```java
int mult(int tal1, int tal2){
    return tal1*tal2;
}
```
**Lav en ny funktion med samme navn “mult”, der modtager tre tal som parametre. Den nye funktion skal anvende funktionen fra spørgsmål 2 til at gange 3 tal sammen**
```java
int mult(int tal1, int tal2, int tal3){
    return mult(mult(tal1, tal2),tal3);
}
```
**(frivillig) Hvad betyder rekursion - prøv at slå det op**

Rekursion er når en funktion kalder sig selv

**(frivillig) Give et eksempel på en funktion, der anvender rekursion. Funktionen skal modtage et tal som parameter og returnere fakultet af tallet. F.eks. beregnes fakultet af 5 således 5! = 5x4x3x2x1**
```java
int fakultet(int tal){
    if (tal == 1) {
        return 1;
    } else {
        return tal*fakultet(tal-1);
    }
}
```

# Meget svære opgaver i funktioner
## Opgave beskrivelse
Lav en rekursiv funktion “int fib(int t)” der kan retunere et bestemt tal i fibonacci-talrækken. F.eks. fib(6) = 5 og fib(8) = 13.
https://da.wikipedia.org/wiki/Fibonacci-tal
https://en.wikipedia.org/wiki/Recursion

Lav en anden funktion, som vha. “fib” tegner følgende mønster:
https://da.wikipedia.org/wiki/Fibonacci-tal#/media/Fil:FibonacciBlocks.svg
## kode 
```java
int fib(int t) {
    if (t == 1 || t <= 0) {
        return 0;
    }
    if (t == 2) {
        return 1;
    }
    
    return fib(t - 1) + fib(t - 2);
}

void setup(){
    colorMode(HSB, 360, 100, 100);
    size(500, 500);
    int size = 0;
    translate(width/2, height/2);
    for (int i = 2; i < 15; i++) {
        size = fib(i)*10;
        fill(size%360, 100, 100);
        println("size: "+size, i, fib(i-1));
        rect(0, 0, size, size);
        rotate(HALF_PI);
        translate(-fib(i-1)*10, 0);
    }
}

```

## Resultat
![](Pasted%20image%2020230929142549.png)


# Largest number
```java
void setup(){
    println("removeIndex: "+removeIndex("1234567", 3));
    println("largest: "+largest("1234567"));
}

String removeIndex(String s, int i) {
    return s.substring(0, i) + s.substring(i+1, s.length());
}

String largest(String s){
    String largest = "";
    for(int i = 0; i < s.length(); i++){
        String temp = removeIndex(s, i);
        if(int(temp) > int(largest)){
            largest = temp;
        }
    }
    return largest;
}
```

# Count in string
```java
void setup(){
    println("countCharInString: "+countCharInString("heje", 'e'));
}

int countCharInString(String str, char c){
    int count = 0;
    for(int i = 0; i < str.length(); i++){
        if(str.charAt(i) == c){
            count++;
        }
    }
    return count;
}
```

# Beauty factor

```java
void setup(){
    println("beautifyOnce: "+beautifyOnce("234"));
    println("beautify: "+beautify("11"));
    exit();
}

int beautifyOnce(String n){
    int sum = 0;
    for(int i = 0; i < n.length(); i++){
        sum += n.charAt(i) - '0';
    }
    return sum;
}

int beautify(String n){
    while(n.length() > 1){
        n = beautifyOnce(n)+"";
    }
    return int(n);
}
```
# min max
```java	
void setup(){
    int[] list1 = {1,2,3,5,4};
    println("contains: "+contains(list1, 1));
    println("min_max: "+min_max(list1));
    exit();
}

boolean contains (int[] arr, int val){
    for (int i = 0; i < arr.length; i++){
        if (arr[i] == val){
            return true;
        }
    }
    return false;
}

boolean min_max(int[] arr){
    int min = arr[0];
    int max = arr[0];
    boolean contains = true;
    for (int i = 0; i < arr.length; i++){
        if (arr[i] < min){
            min = arr[i];
        }
        if (arr[i] > max){
            max = arr[i];
        }
    }
    for(int i = min; i < max; i++){
        if (!contains(arr, i)){
            return false;
        }
    }
    return contains;
}
```

# objektorienteret programmering

**Forklar hvad der menes med “class”**

En class er en blueprint eller template for et objekt

**Forklar hvad der menes med “object”**

Et objekt er en instans af en class

**Forklar hvordan og hvorfor man anvender “new”**

Laver et "new" (nyt) objekt ud fra en class

**Forklar hvad er “dot-syntax”**

Hvis man skal refere til noget på objektet (f.eks funktions and variables)

**Hvad er en “constructor”**

En constructor er en særlig funktion i en class, som bliver kaldt når man laver et nyt objekt. Man kan også sige at den bliver 
brugt til at initialisere objektet.

## Kode
```java
Bubble[] bubbles = new Bubble[10];

void setup() {
  size(480, 270);
    for(int i = 0; i < 10; i++) {
      bubbles[i] = new Bubble(random(5,50));
    }
}

void draw() {
  background(255);
  for(Bubble b : bubbles) {
    b.ascend();
    b.display();
  }
}


class Bubble {

  float x;
  float y;
  float diameter;

  Bubble(float _diameter) {
    x = width/2;
    y = height;
    diameter = _diameter;
  }

  void ascend() {
    y--;
    x = x + random(-2,2);
    top();
  }

  void display() {
    stroke(0);
    fill(127);
    ellipse(x, y, diameter, diameter);
  }

  void top() {
    if (y < diameter/2) {
      y = diameter/2;
    }
  }
}

```


# Opgaver i funktions terminologi

**Opgave 1: Forklar begrebet funktion i programmering, herunder betydningen af et funktionskald. Giv et eksempel.**

  En function er en kodeblok som kan bruges flere gange. Når man køre koden i en function, så kaldes det et funktionskald. Se opgave 5 for eksempel.
 
**Opgave 2: Definér parametre, argumenter og metode-krop i programmering. Giv et eksempel**
 
 Parametre er variabler man kan parse til funktionen. Argumenter er værdierne som bliver sendt til funktionen. Metode-krop er koden som bliver kørt i funktionen. Se opgave 5 for eksempel.

**Opgave 3: Forklar begrebet variabel-scope i programmering. Og forskellen på lokale variable og globale variable. Giv et eksempel**

   Variabel-scope er hvor en variabel kan bruges. Lokale variable kan kun bruges i den function de er defineret i. Globale variable kan bruges i hele programmet.

**Opgave 4: Definér returtype og returværdi i programmering.**

  Returtype er typen af værdi som bliver returneret. Returværdi er værdien som bliver returneret.
# Opgaver i programmering af funktioner

```java
// Opgave 5: Skab “givHilsen”, en funktion med to inputparametre: en liste af hilsner og et tal, der bestemmer hvilken hilsen der skal returneres.

String givHilsen(String[] hilsner, int tal) {

    return hilsner[tal];

}

// Opgave 6: Implementer “beregnAreal”, en funktion til at beregne og returnere arealet af en vilkårlig cirkel.

double beregnAreal(double radius) {

    return Math.PI * Math.pow(radius, 2);

}

// Opgave 7: Skriv en funktion, der kan håndtere et vilkårligt antal punkter og skabe en tegning, der forbinder dem.

void tegnLinje(PVector[] punkter) {

    for (int i = 0; i < punkter.length-1; i++) {

            line(punkter[i].x, punkter[i].y, punkter[i + 1].x, punkter[i + 1].y);

    }

}

// Opgave 8: Frivillig: Udvikl en funktion, der kan tegne en vilkårlig N-kant med et valgfrit centrum.

void tegnPolygon(PVector[] punkter, float x, float y) {

    for (int i = 0; i < punkter.length; i++) {

            line(punkter[i].x+x, punkter[i].y+y, punkter[(i + 1)%punkter.length].x+x, punkter[(i + 1)%punkter.length].y+y);

    }

}
```