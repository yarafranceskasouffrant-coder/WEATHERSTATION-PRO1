# WEATHERSTATION-PRO1
Smart weather monitoring system built with Raspberry Pi Pico and MicroPython featuring DHT22, BMP280, MQ-135 sensors, OLED interface, RGB alerts, buzzer alarms, and automatic ventilation control.
# WeatherStation Pro - Station météo automatisée

## Membres du groupe
| Nom | Rôle |
| :--- | :--
| **ETIENNE Maxi Christopher** | Responsable câblage et Validation Wokwi |
| **SOUFFRANT Yara Franceska** | Responsable Tests et Documentation GitHub |

## Description du projet
WeatherStation Pro est une station météo intelligente conçue avec un Raspberry Pi Pico et plusieurs capteurs environnementaux. Le système mesure en temps réel la température, l’humidité, la pression atmosphérique et la qualité de l’air dans différentes zones. Toutes les informations sont affichées sur un écran OLED avec une navigation entre plusieurs interfaces grâce à des boutons poussoirs. En cas de danger ou d’anomalie, une LED RGB, un buzzer et un servomoteur réagissent automatiquement pour simuler un système d’alerte et de ventilation.

## Lien de simulation Wokwi
Cliquez ici: https://wokwi.com/projects/464194700139737089

## Capture d'écran de la simulation
![Simulation](images/<img width="800" height="902" alt="121_edited" src="https://github.com/user-attachments/assets/08db8f4d-5f30-4b58-977e-4f407c8498ad" />
.png)

## Composants utilisés
| Composant | Quantité | Rôle |
| :--- | :---: | :--- |
| Raspberry Pi Pico | 1 | [cite_start]Cerveau principal du système (MicroPython) |
| Capteur DHT22 | 2 | [cite_start]Mesure de la température et de l'humidité (Zone 1 et Zone 2) |
| Capteur BMP180 (I2C) | 1 | [cite_start]Mesure de la pression atmosphérique et de la température  |
| Capteur MQ-135 | 1 | [cite_start]Capteur de qualité de l'air / niveau de CO2  |
| Écran OLED SSD1306 (I2C) | 1 | [cite_start]Affichage des mesures et de l'historique en temps réel  |
| LED RGB (Cathode commune) | 1 | [cite_start]Indicateur visuel de l'état global (Vert: OK, Rouge: Alerte)  |
| Servomoteur SG90 | 1 | [cite_start]Simulation mécanique de l'ouverture d'une ventilation  |
| Buzzer passif | 1 | [cite_start]Émission de signaux sonores d'alerte en cas de danger |
| Bouton poussoir | 2 | [cite_start]Navigation entre les menus OLED et réinitialisation  |
| Résistances 220 Ohm | 3 | [cite_start]Protection de la LED RGB contre les surintensités  |
| Résistances 10 kOhm | 2 | [cite_start]Résistances de pull-up pour la stabilisation des boutons  |
| Potentiomètre | 1 | [cite_start]Simulation analogique des variations de la qualité de l'air (CO2)  |
| Breadboard grande | 1 | [cite_start]Support de prototypage pour les connexions sans soudure  |
| Câbles Dupont | 35 | [cite_start]Fils d'interconnexion pour relier les composants au Pico  |

## Répartition du travail
| Étudiant | Tâches réalisées |
| :--- | :--- |
| **ETIENNE Maxi Christopher** | Implantation matérielle sur la breadboard virtuelle Wokwi, interconnexion des bus I2C et câblage/validation générale de la simulation. |
| **SOUFFRANT Yara Franceska** | Exécution des plans de test, vérification des seuils d'alerte, création du dépôt GitHub et gestion de la documentation du projet. |

## Tests réalisés
| Test | Résultat attendu | Résultat obtenu | 
| :--- | :---: | :---: |
| Appui sur le bouton de navigation | [cite_start]L'écran OLED bascule fluidement entre les 4 menus (Zones, Air, Historique...)  | L'affichage change instantanément à chaque clic sans saut 
| Température ou humidité > Seuils | [cite_start]La LED change de couleur, le buzzer sonne et le servomoteur s'active à 90°  | La LED bascule, l'alerte sonore se déclenche et la ventilation s'ouvre
| Déconnexion d'un capteur DHT22 | Le programme continue de tourner grâce au bloc `try/except` sans planter | Le système reste actif et capture l'erreur en arrière-plan 
| Stabilisation logique (Gaz/Air) | Ignorer les fluctuations de tension furtives à l'aide d'un filtrage dans le code | Les pics isolés sont filtrés, évitant les déclenchements d'alerte erronés 

## Améliorations possibles
* **Filtrage temporel par persistance :** Implémentation d'une fonction de vérification qui attend plusieurs lectures consécutives de danger avant de déclencher l'alarme pour éliminer les fausses alertes.
* **Moyennage glissant :** Stockage des dernières mesures dans un tableau FIFO (First In, First Out) pour lisser les données brutes des capteurs environnementaux.
* **Sauvegarde Flash (Log) :** Enregistrement local de l'historique des alertes directement dans la mémoire flash du Raspberry Pi Pico pour conserver les données en cas de coupure de courant.

## Difficultés rencontrées
* **`ImportError` sur la bibliothèque SSD1306 :** Problème résolu en ajoutant manuellement le fichier de pilote autonome `ssd1306.py` dans l'interface de simulation de Wokwi.
* **Erreurs de syntaxe `IndentationError` :** Problèmes d'alignement des lignes de code lors des copier-coller sur navigateur, corrigés en réalignant strictement les blocs de la boucle principale et des exceptions.
