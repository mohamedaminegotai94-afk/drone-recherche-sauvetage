# Répartition du travail du binôme

## Mohamed Amine — Simulation, intégration et navigation

- Créer le bâtiment, les obstacles et le drone dans Gazebo.
- Configurer PX4 SITL et l’intégration avec ROS 2.
- Publier la pose, la vitesse et l’état du drone.
- Développer les commandes de déplacement et une couche de sécurité simple.
- Mettre en place la navigation de référence, puis intégrer PPO/VARE si le calendrier le permet.

**Livrable principal :** un drone simulé qui se déplace dans le bâtiment, publie son état et suit des consignes vérifiées par la couche de sécurité.

## Bille — Perception et écran opérateur

- Récupérer et afficher les images de la caméra.
- Intégrer la détection de personnes potentielles.
- Enregistrer chaque observation avec son image, son horodatage et son score.
- Développer l’écran opérateur : vidéo, carte, position du drone, état de mission et signalements.
- Associer les détections à une position estimée sur la carte lorsque la profondeur et la pose sont disponibles.

**Livrable principal :** un responsable peut suivre la simulation, voir les observations et signaler une personne potentielle ou un danger.

## Travail commun

- Définir ensemble les interfaces ROS 2 et les formats de données avant l’intégration.
- Tester régulièrement les deux parties ensemble.
- Préparer les scénarios, les métriques, les expériences comparatives et le rapport.

## Premier test d’intégration

Afficher simultanément une image caméra, la position du drone et un signalement horodaté. Une partie peut utiliser des données fictives pendant que l’autre termine son module, puis les deux modules sont connectés.
