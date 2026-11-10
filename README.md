# Drone autonome de recherche et de sauvetage en milieu sinistré

## Présentation du projet

Ce projet porte sur la conception et l’évaluation **en simulation** d’un drone d’exploration destiné aux bâtiments dangereux, par exemple après un séisme ou un incendie. Le drone doit aider les équipes de secours en explorant des zones difficiles d’accès et en transmettant les informations utiles à un responsable qui reste à distance.

Le système visé combine plusieurs fonctions : navigation dans le bâtiment, transmission de la vidéo, détection de personnes potentielles, localisation des observations sur une carte et évitement des obstacles. L’exploration doit progressivement tenir compte des zones déjà visitées, des indices de présence humaine et du risque du trajet.

Le projet est évalué dans un environnement simulé. Il ne constitue pas une validation pour une intervention dans un vrai incendie ou un bâtiment instable.

## Objectifs

- Construire un bâtiment sinistré et un quadricoptère dans un simulateur.
- Recevoir les images et les informations de position du drone.
- Afficher la vidéo, la carte, la position et les signalements sur un écran opérateur.
- Détecter des personnes potentielles dans les images.
- Estimer la position des observations à l’aide de la profondeur et de la pose du drone.
- Développer une navigation qui évite les obstacles et limite les déplacements inutiles.
- Comparer différentes stratégies d’exploration à l’aide de mesures reproductibles.

## Fonctionnement envisagé

1. Gazebo simule le bâtiment, le drone, les capteurs et les obstacles.
2. PX4 SITL assure le contrôle de vol dans la simulation.
3. ROS 2 transmet les images, la pose, les détections et les commandes entre les modules.
4. Le module de perception signale les personnes potentielles observées par la caméra.
5. Le module de cartographie associe les observations à la carte lorsque les informations de profondeur et de position le permettent.
6. Le planificateur choisit les zones à explorer ; la couche de sécurité vérifie les commandes avant leur exécution.
7. L’écran opérateur présente la vidéo, la position estimée du drone, les observations et l’état de la mission.

## Technologies envisagées

- **Gazebo** : simulation du bâtiment et du drone.
- **PX4 SITL** : autopilote simulé.
- **ROS 2** : communication entre les composants.
- **Python, OpenCV et YOLO/PyTorch** : traitement des images et détection.
- **A* et exploration par frontières** : méthodes de référence pour la navigation.
- **PPO et éventuellement VARE** : exploration intelligente à évaluer.

Les versions de Gazebo, PX4 et ROS 2 devront être choisies dans une combinaison compatible, puis documentées dans le dépôt.

## Répartition du travail

### Mohamed Amine — Simulation, vol et navigation

- Créer le bâtiment, les obstacles et le drone dans Gazebo.
- Configurer PX4 SITL et son intégration avec ROS 2.
- Récupérer et publier la pose, la vitesse et l’état du drone.
- Développer les commandes de déplacement et une première couche de sécurité.
- Mettre en place une méthode de navigation de référence, puis travailler sur PPO/VARE si le calendrier le permet.

### Bille — Perception et écran opérateur

- Récupérer et afficher la vidéo de la caméra.
- Intégrer la détection de personnes potentielles.
- Associer les détections à une position estimée sur la carte lorsque la profondeur et la pose sont disponibles.
- Créer l’écran opérateur : vidéo, carte, position, état de mission et signalements.
- Enregistrer les observations avec leur image et leur horodatage.

### Travail commun

- Définir les interfaces ROS 2 et les formats de données.
- Intégrer et tester les modules ensemble dès le début.
- Préparer les scénarios d’essai, analyser les résultats et rédiger le rapport.

## Organisation du dépôt

```text
drone-recherche-sauvetage/
├── README.md
├── docs/                 # Architecture, répartition, planning et interfaces
├── simulation/           # Mondes Gazebo et notes de simulation
├── ros2_ws/src/          # Futurs packages ROS 2
├── dashboard/            # Écran opérateur
├── data/                 # Informations sur les jeux de données
└── experiments/           # Scénarios, métriques et résultats
```

## État actuel

Le dépôt contient la documentation initiale et la structure de travail. Les nœuds ROS 2, les mondes Gazebo et l’écran opérateur restent à développer.

## Limites et sécurité

La pose fournie par Gazebo peut être utilisée pour les premiers essais, mais elle ne doit pas être présentée comme une validation du SLAM. Dans un vrai bâtiment, le GPS intérieur n’est pas une solution suffisante et une méthode de localisation adaptée serait nécessaire. Une détection automatique indique une **personne potentielle** ; elle ne confirme pas à elle seule la présence d’une victime.
