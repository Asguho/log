
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
            printInMiddle("W");
        break;  
        case 1 :
            printInMiddle("S");
        break;
        case 0 :
            printInMiddle("E");
        break;
        case -1 :
            printInMiddle("N");
        break;
    }
}
  
void printInMiddle(String s) {
    textSize(128);
    fill(0);
    // text(s,width / 2-textWidth(s)/2,height / 2+(textAscent()+textDescent())/2);
    textAlign(CENTER, CENTER);
    text(s, width / 2, height / 2);  
}
```
### Resultat
![](Pasted%20image%2020230823124320.png)