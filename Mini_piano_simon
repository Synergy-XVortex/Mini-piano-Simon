// Mise en place des constantes
const int LED_0 = 11;   // Pin pour la LED 0
const int Button_0 = 2; // Pin pour le bouton 0

const int LED_1 = 10;    // Pin pour la LED 1
const int Button_1 = A0; // Pin pour le bouton 1

const int LED_2 = 9;     // Pin pour la LED 2
const int Button_2 = A1; // Pin pour le bouton 2

const int LED_3 = 8;     // Pin pour la LED 3
const int Button_3 = A2; // Pin pour le bouton 3

const int LED_4 = 7;     // Pin pour la LED 4
const int Button_4 = A3; // Pin pour le bouton 4

const int LED_5 = 6;     // Pin pour la LED 5
const int Button_5 = A4; // Pin pour le bouton 5

const int LED_6 = 5;     // Pin pour la LED 6
const int Button_6 = A5; // Pin pour le bouton 6

const int LED_Vert = 13;     // Pin pour la LED verte
const int LED_Rouge = 12;    // Pin pour la LED rouge
const int Button_Switch = 4; // Pin pour le bouton de mode
const int Buzzer = 3;        // Pin pour le buzzer

bool jeu = true; // Variable pour indiquer si le jeu est en cours
bool verif =
    false; // Variable pour vérifier si l'utilisateur a appuyé sur le bon bouton
int nombre = 0; // Variable pour indiquer le nombre de boutons que l'utilisateur
                // doit appuyer
int tour = 0;   // Variable pour indiquer le tour actuel du jeu
int pin = 0;    // Variable pour stocker la pin correspondant au bouton appuyé
bool buttonState = false; // Variable pour indiquer l'état du bouton de mode

// Création de la liste des fréquences des différentes notes
int notes[] = {1567, 1661, 1760, 1864, 1975, 2093, 2217};

// Tableau pour stocker la séquence de boutons générée par le jeu
int valeur[100];

// Fonction setup
void setup() {
  // Initialisation de la communication série à 9600 bauds
  Serial.begin(9600);

  // Configuration des pins pour les LED et le buzzer
  for (int i = 3; i < 14; i++) {
    pinMode(i, OUTPUT);
  }

  // Configuration des pins pour les boutons
  pinMode(4, INPUT);  // Bouton Switch mode
  pinMode(2, INPUT);  // Bouton 0
  pinMode(A0, INPUT); // Bouton 1
  pinMode(A1, INPUT); // Bouton 2
  pinMode(A2, INPUT); // Bouton 3
  pinMode(A3, INPUT); // Bouton 4
  pinMode(A4, INPUT); // Bouton 5
  pinMode(A5, INPUT); // Bouton 6
}

// Fonction loop
void loop() {
  if (digitalRead(Button_Switch) == HIGH) // Bouton Switch pour lancer le jeu
  {
    buttonState = !buttonState; // inverser l'état du bouton
    delay(500);                 // attendre un peu pour éviter les rebonds
  }
  while (buttonState == true) // tant que le bouton est activé
  {
    melodieLancement();    // joue une mélodie pour indiquer le début du jeu
    buttonState = simon(); // lance le jeu de Simon
  }
  if (buttonState == false) // si le bouton n'est pas activé
  {
    button(); // lire les entrées de bouton pour ajouter des coups
  }
}

// Fonction pour l'allumage des Led et la production du son
void note(int pin) {
  digitalWrite(11 - pin, HIGH); // Allume la LED correspondante à la note
  tone(Buzzer, notes[pin],
       200);   // Joue la note avec une durée de 200ms sur le buzzer
  delay(1000); // Attend une seconde
  digitalWrite(11 - pin, LOW); // Éteint la LED correspondante à la note
}

// Fonction alternative pour jouer une note plus rapidement
void note1(int pin) {
  digitalWrite(11 - pin, HIGH); // Allume la LED correspondante à la note
  tone(Buzzer, notes[pin],
       200);  // Joue la note avec une durée de 200ms sur le buzzer
  delay(100); // Attend 100ms
  digitalWrite(11 - pin, LOW); // Éteint la LED correspondante à la note
}

// Fonction button
void button() {
  if (digitalRead(Button_0) == HIGH) // Si le bouton 0 est appuyé
  {
    pin = 0;             // On stocke la valeur de la note correspondante
    note1(pin);          // On joue la note
    Serial.println("1"); // On affiche "1" sur le moniteur série
  }
  if (digitalRead(Button_1) == HIGH) // Si le bouton 1 est appuyé
  {
    pin = 1;    // On stocke la valeur de la note correspondante
    note1(pin); // On joue la note
  }
  if (digitalRead(Button_2) == HIGH) // Si le bouton 2 est appuyé
  {
    pin = 2;    // On stocke la valeur de la note correspondante
    note1(pin); // On joue la note
  }
  if (digitalRead(Button_3) == HIGH) // Si le bouton 3 est appuyé
  {
    pin = 3;    // On stocke la valeur de la note correspondante
    note1(pin); // On joue la note
  }
  if (digitalRead(Button_4) == HIGH) // Si le bouton 4 est appuyé
  {
    pin = 4;    // On stocke la valeur de la note correspondante
    note1(pin); // On joue la note
  }
  if (digitalRead(Button_5) == HIGH) // Si le bouton 5 est appuyé
  {
    pin = 5;    // On stocke la valeur de la note correspondante
    note1(pin); // On joue la note
  }
  if (digitalRead(Button_6) == HIGH) // Si le bouton 6 est appuyé
  {
    pin = 6;    // On stocke la valeur de la note correspondante
    note1(pin); // On joue la note
  }
}

// Fonction check
int check(int pin, int nombre) {
  if (pin ==
      valeur[nombre]) // Si le bouton pressé correspond à la séquence attendue
  {
    nombre += 1; // On incrémente la position dans la séquence attendue
    return (
        nombre); // On retourne la nouvelle position dans la séquence attendue
    delay(500);  // On attend 500ms avant de continuer
  } else if (pin != valeur[nombre]) // Si le bouton pressé ne correspond pas à
                                    // la séquence attendue
  {
    ledrouge();      // On allume la LED rouge pour signaler une erreur
    nombre = -1;     // On réinitialise la position dans la séquence attendue
    return (nombre); // On retourne la nouvelle position dans la séquence
                     // attendue (qui sera -1 en cas d'erreur)
    delay(500);      // On attend 500ms avant de continuer
  }
}

// Fonction add : ajoute la valeur de la LED appuyée dans le tableau "valeur" et
// incrémente le nombre de tours effectués
int add(int pin, int nombre) {
  valeur[nombre] =
      pin;    // Ajoute la valeur de la LED appuyée dans le tableau "valeur" à
              // l'indice correspondant au nombre de tour effectué
  tour += 1;  // Incrémente le nombre de tours effectués
  nombre = 0; // Réinitialise le compteur du nombre de notes à vérifier
  return (nombre); // Retourne la nouvelle valeur du compteur
}

// Fonction melodieLancement : joue une mélodie et allume toutes les LEDs pour
// signaler le début du jeu
void melodieLancement() {
  digitalWrite(LED_0, HIGH);
  tone(Buzzer, notes[0]);
  delay(300);
  digitalWrite(LED_1, HIGH);
  tone(Buzzer, notes[1]);
  delay(300);
  digitalWrite(LED_2, HIGH);
  tone(Buzzer, notes[2]);
  delay(300);
  digitalWrite(LED_3, HIGH);
  tone(Buzzer, notes[3]);
  delay(300);
  digitalWrite(LED_4, HIGH);
  tone(Buzzer, notes[4]);
  delay(300);
  digitalWrite(LED_5, HIGH);
  tone(Buzzer, notes[5]);
  delay(300);
  digitalWrite(LED_6, HIGH);
  tone(Buzzer, notes[6]);
  delay(300);
  noTone(Buzzer);
  for (int i = 5; i < 12; i++) // Éteint toutes les LEDs
  {
    digitalWrite(i, LOW);
  }
}

// Fonction ledverte : allume la LED verte et joue une note pour signaler une
// réponse correcte
void ledverte() {
  digitalWrite(LED_Vert, HIGH); // Allume la LED verte
  tone(Buzzer, 523);            // Joue la note DO
  delay(500);
  digitalWrite(LED_Vert, LOW); // Éteint la LED verte
  noTone(Buzzer);              // Arrête le son
}

// Fonction ledrouge : allume la LED rouge et joue une mélodie pour signaler une
// réponse incorrecte
void ledrouge() {
  digitalWrite(LED_Rouge, HIGH); // Allume la LED rouge
  tone(Buzzer, 1175);            // Joue la note RE#
  delay(250);
  noTone(Buzzer);    // Arrête le son
  tone(Buzzer, 988); // Joue la note SI
  delay(250);
  noTone(Buzzer);    // Arrête le son
  tone(Buzzer, 880); // Joue la note LA
  delay(250);
  noTone(Buzzer);               // Arrête le son
  digitalWrite(LED_Rouge, LOW); // Éteint la LED rouge
}

// Fonction simon
//  Fonction simon
bool simon() {
  jeu = true; // Initialisation des variables
  verif = false;
  nombre = 0;
  tour = 0;
  pin = 0;
  int valeur[100]; // Tableau pour stocker la séquence

  while (jeu == true) // Boucle principale du jeu
  {
    if (nombre == -1) // Si l'utilisateur arrête le jeu
    {
      digitalWrite(LED_Rouge, LOW); // Éteindre toutes les LED
      digitalWrite(LED_Vert, LOW);
      jeu = false; // Sortir de la boucle
      return (jeu);
      delay(500); // Attendre un peu
    }

    // Alterner les LED pour indiquer quel joueur doit jouer
    if (tour % 2 == 0) {
      digitalWrite(LED_Rouge, LOW);
      digitalWrite(LED_Vert, HIGH);
    }
    if (tour % 2 == 1) {
      digitalWrite(LED_Vert, LOW);
      digitalWrite(LED_Rouge, HIGH);
    }

    if (nombre == tour && verif == true) // Indicateur disant si la séquence est
                                         // correcte à la fin du tour
    {
      ledverte();    // Faire clignoter la LED verte
      verif = false; // Réinitialiser le vérificateur
      delay(500);
    }

    // Si le tour n'est pas terminé et que la réponse est correcte, attendre
    // l'ajout d'une nouvelle note
    if (nombre == tour && verif == false) {
      // Vérifier quel bouton a été appuyé pour ajouter une nouvelle note à la
      // séquence à répéter
      if (digitalRead(Button_0) == HIGH) // Si le bouton 0 est pressé
      {
        pin = 0;                   // Stocke la valeur 0 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }

      if (digitalRead(Button_1) == HIGH) // Si le bouton 1 est pressé
      {
        pin = 1;                   // Stocke la valeur 1 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }

      if (digitalRead(Button_2) == HIGH) // Si le bouton 2 est pressé
      {
        pin = 2;                   // Stocke la valeur 2 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }

      if (digitalRead(Button_3) == HIGH) // Si le bouton 3 est pressé
      {
        pin = 3;                   // Stocke la valeur 3 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }

      if (digitalRead(Button_4) == HIGH) // Si le bouton 4 est pressé
      {
        pin = 4;                   // Stocke la valeur 4 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }

      if (digitalRead(Button_5) == HIGH) // Si le bouton 5 est pressé
      {
        pin = 5;                   // Stocke la valeur 5 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }

      if (digitalRead(Button_6) == HIGH) // Si le bouton 6 est pressé
      {
        pin = 6;                   // Stocke la valeur 6 dans la variable "pin"
        note(pin);                 // Joue la note correspondante
        nombre = add(pin, nombre); // Ajoute la valeur à la séquence et
                                   // incrémente la variable "nombre"
      }
    }

    if (nombre < tour) // Si c'est le tour de vérifier la séquence
    {
      verif = true;                      // Active la vérification
      if (digitalRead(Button_0) == HIGH) // Si le bouton 0 est pressé
      {
        pin = 0;   // Stocke la valeur 0 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }

      if (digitalRead(Button_1) == HIGH) // Si le bouton 1 est pressé
      {
        pin = 1;   // Stocke la valeur 1 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }

      if (digitalRead(Button_2) == HIGH) // Si le bouton 2 est pressé
      {
        pin = 2;   // Stocke la valeur 2 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }

      if (digitalRead(Button_3) == HIGH) // Si le bouton 3 est pressé
      {
        pin = 3;   // Stocke la valeur 3 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }

      if (digitalRead(Button_4) == HIGH) // Si le bouton 4 est pressé
      {
        pin = 4;   // Stocke la valeur 4 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }

      if (digitalRead(Button_5) == HIGH) // Si le bouton 5 est pressé
      {
        pin = 5;   // Stocke la valeur 5 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }

      if (digitalRead(Button_6) == HIGH) // Si le bouton 6 est pressé
      {
        pin = 6;   // Stocke la valeur 6 dans la variable "pin"
        note(pin); // Joue la note correspondante
        nombre = check(pin, nombre); // Vérifie la valeur et incrémente la
                                     // variable "nombre" si elle est correcte
        delay(500); // Temps de latence avant la prochaine vérification
      }
    }
  }
}
