---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---

# Lezione 4

I led RGB e il ciclo

---

# Cos'è un led RGB?

Un led RGB è un LED particolare che può assumere tutti i colori.

Per cambiare colore andiamo a miscelare i 3 colori che il LED ci mette a disposizione: Rosso, Verde e Blu.

<div flex >
  <div>
    <img src="https://dwma4bz18k1bd.cloudfront.net/tutorials/Common-Anode-RGB-LED-Pinout.png" width="1200"/>
  </div>
  <div pt-10>
Quindi è come se fosse composto da 3 LED uno rosso, uno verde e uno blu. Miscelando questi 3 colori possiamo visualizzare una buona quantità di colori.
  </div>
</div>

Inoltre abbiamo un pin positivo come un LED monocolore per portare la corrente ai 3 LED.
---

# Come misceliamo i colori?


Per miscelare i colori del LED RGB usiamo quindi 3 potenziometri che regolerenno la quantità di colore per formarne di altri.

<img src="https://github.com/ArduinoAgnelli/Progetti/blob/main/potenziometro-rgb/schema-arduino.png?raw=true" width="800"/>
Notate che ogni colore avrà una resistenza proprio perchè sono 3 LED separati

---

# Il codice

Il codice per il led RGB è il seguente: 

```c
#define POTGREEN A0 // Il potenziometro che controllerà il led verde
#define POTBLUE A1  // Il potenziometro che controllerà il led blue
#define POTRED A2 // Il potenziometro che controllerà il led rosso
#define GREEN 3
#define BLUE 5
#define RED 6
void setup()
{
  pinMode(POTGREEN, INPUT); // Inizializziamo i vari pin
  pinMode(POTBLUE, INPUT);
  pinMode(POTRED, INPUT);
  pinMode(GREEN, OUTPUT);
  pinMode(BLUE, OUTPUT);
  pinMode(RED, OUTPUT);
}
void loop()
{
  analogWrite(GREEN,analogRead(POTGREEN)/4);  // Scriviamo il valore dei potenziometri nei corrispettivi LED
  analogWrite(BLUE,analogRead(POTBLUE)/4);
  analogWrite(RED,analogRead(POTRED)/4);
}
```

---

# Immettiamo dei valori fissi


```c
#define GREEN 3
#define BLUE 5
#define RED 6
void setup()
{
  pinMode(GREEN, OUTPUT);
  pinMode(BLUE, OUTPUT);
  pinMode(RED, OUTPUT);
}
void loop()
{
  analogWrite(GREEN,100);  // Scriviamo dei valori fissi nei vari LED
  analogWrite(BLUE,200);
  analogWrite(RED,50);
}
```

Provate a modificare i valori

---

# Valori casuali

Per generare dei valori casuali usiamo il seguente codice:

```c
srand(time(NULL));  // Questo serve solo una volta
rand() % 100
```
Che quindi genererà un valore casuale tra 0 e 100. 
Se vogliamo generare dei numeri casuali per dei led RGB useremo questo codice: 

```c
#define GREEN 3
#define BLUE 5
#define RED 6
void setup()
{
  pinMode(GREEN, OUTPUT);
  pinMode(BLUE, OUTPUT);
  pinMode(RED, OUTPUT);
}
void loop()
{
  srand(time(NULL));
  analogWrite(GREEN,rand()%255);  // Scriviamo dei valori casuali nei vari LED
  analogWrite(BLUE,rand()%255);
  analogWrite(RED,rand()%255);
}
```


---

# Il ciclo FOR


Il ciclo FOR esegue delle determinate istruzione per un determinato numero di volte, ecco qui un esempio che crea un effetto LED:

```c
#define INIZIO 0
#define FINE 7

void setup() {
  for (int i = INIZIO; i <= FINE; i++) {
  	pinMode(i, OUTPUT);
  }
}

void loop() {
  for (int i = INIZIO; i <= FINE; i++) {
  	digitalWrite(i, HIGH);
    delay(250);
  }
  
  for (int i = INIZIO; i <= FINE; i++) {
  	digitalWrite(i, LOW);
    delay(250);
  }
}
```

Provate a creare nuovi effetti usando anche i led RGB
