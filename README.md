# Orchestrion_Plucked_Strings_Servomotors

Le projet permet de controller un instrument à cordes grattée (guitare, basse, ukulele, etc ...) en utilisant des servomoteurs pour actionner les frettes et gratter les cordes en fonction des messages midi recu via usb.  

le code est construit de facon objet et se veut adaptable pour touts les cas d'utilisations il suffira d'adapter les paramettres du fichier settings.h en fonction du branchement choisis.

le code de ce projet est contruit autour de cartes PCA9685 controlé via i2c
<img src="https://raw.githubusercontent.com/glloq/Orchestrion_Plucked_Strings_Servomotors/main/img/Schemas.png?raw=true" alt="controle via pca" width=80% height=80%/>  

### accords
nous pouvons utiliser plusieurs methodes pour actionner les frettes sur la corde, voici un exemple caché
<img src="https://github.com/glloq/OneStringGuitar/blob/main/img/fingers%20servo.png" alt="Your image title" width=80% height=80%/>

### grattage 
on peut utiliser un servomoteur pour gratter en direct ou en deporté en alternant entre 2 angles entre chaque grattage de la corde.
on peut aussi utiliser le servomoteur pour etoufer la note en remetant le pick contre la corde a la reception d'un message noteOff.   
<img src="https://github.com/glloq/OneStringGuitar/blob/main/img/grattage%20servo.png" alt="grattage servo" width=60% height=60%/>

## configuration de l'instrument 

le code permet de s'adapter a tout les cas d'utilisations, il suffit d'indiquer le nombre de cordes de l'instrument, le nombre de mcp utilisé et l'angle d'activation de la frette et le sens de fonctionnement.

```
#define NUM_STRINGS 4         // Nombre de cordes
#define PCA_NUMBER_USED 4      // Nombre de pca à initialiser
#define PIN_UNPOWER_SERVO 4      // pin vers oe du pca9685

```
la definition de chaque corde est faite dans le tableau de cordes stringConfigs[NUM_STRINGS]
il suffira d'ajouter le meme nombre de lignes que de nombre de corde  avec les differentes informations de chaque corde
```
struct StringConfig {
  int midiNote;          // Numéro MIDI de la corde à vide
  int fretsNumbers;      // Nombre de frettes utilisées sur la corde
  int pinFirstFret;      // Pin PCA de la première frette
  int pinServoPluck;     // Pin pour le servo de grattage
  int AngleServoPluck;   // angle servo de grattage contre la corde
  int angleServoFret[fretsNumbers]; // angle de chaque servomoteur pour actionner la frette
  bool sensServoFret[fretsNumbers]; // sens de rotation pour desactiver la frette
};
```
