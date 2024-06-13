# Projet Mini Piano Simon
Le projet Mini Piano Simon est une implémentation du jeu de mémoire Simon sur Arduino, où les utilisateurs doivent répéter une séquence croissante de notes et de lumières. Voici une décomposition structurée du projet :

# Constantes et Broches
  - LEDs et Boutons :
      - LEDs : Utilisées pour indiquer les notes et le statut du jeu.
          - LED_0 à LED_6 pour les LEDs correspondant aux notes.
          - LED_Vert pour la LED verte indiquant une réponse correcte.
          - LED_Rouge pour la LED rouge indiquant une réponse incorrecte.
      - Boutons : Utilisés pour lire les entrées des utilisateurs.
          - Button_0 à Button_6 pour les boutons correspondant aux notes.
          - Button_Switch pour le bouton de mode de jeu.
  - Autres Composants :
      - Buzzer (Buzzer) : Utilisé pour jouer les notes.

Variables de Contrôle du Jeu
  - Variables Booléennes :
      - jeu : Indique si le jeu est en cours.
      - verif : Indique si l'utilisateur a appuyé sur le bon bouton.
  - Variables de Suivi du Jeu :
      - nombre : Nombre de boutons que l'utilisateur doit appuyer.
      - tour : Tour actuel du jeu.
      - pin : Stocke la valeur du bouton appuyé.
      - buttonState : État du bouton de mode de jeu.

# Fonctions Principales
1. setup() :
    - Initialise la communication série et configure les broches pour les LEDs, les boutons et le buzzer.
    - Allume toutes les LEDs pour signaler le début du jeu.

2. loop() :
    - Boucle principale du programme.
    - Attente de l'appui sur le bouton Switch pour démarrer le jeu.
    - Lance le jeu de Simon et lit les entrées utilisateur.

3. note(int pin) :
    - Allume la LED correspondant à la note et joue la note sur le buzzer pendant 200ms.
    - Attend ensuite 1000ms avant d'éteindre la LED.

4. button() :
    - Lit l'état des boutons et joue la note correspondante lorsque l'un des boutons est pressé.

5. check(int pin, int nombre) :
    - Vérifie si le bouton pressé correspond à la séquence attendue.
    - Allume la LED verte si correct ou la LED rouge si incorrect.
    - Gère les réponses de l'utilisateur et met à jour les variables en conséquence.

6. add(int pin, int nombre) :
    - Ajoute la valeur du bouton appuyé à la séquence à répéter et incrémente le nombre de tours.

7. melodieLancement() :
    - Joue une mélodie et allume toutes les LEDs pour signaler le début du jeu.

8. ledverte() et ledrouge() :
    - Allume la LED verte ou rouge pour signaler une réponse correcte ou incorrecte.
    - Joue des mélodies distinctes correspondant à chaque état.

9. simon() :
    - Boucle principale du jeu Simon.
    - Gère la génération de la séquence, la vérification des réponses utilisateur et l'affichage visuel et sonore en conséquence.

# Conclusion
Le projet Mini Piano Simon sur Arduino combine l'utilisation de LEDs, de boutons et d'un buzzer pour recréer le célèbre jeu de mémoire Simon. En utilisant des fonctions et des boucles, le programme guide l'utilisateur à travers une séquence croissante de notes à répéter, fournissant un retour visuel et sonore instantané sur la précision des réponses.

# Auteur
Ce projet a été développé par Clément Vongsanga. Pour toute question, suggestion ou contribution, n'hésitez pas à ouvrir une issue ou à proposer une pull request sur GitHub.
