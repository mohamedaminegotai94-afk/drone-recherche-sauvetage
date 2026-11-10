# Écran opérateur

Écran prévu pour un responsable de mission, d'abord local sur le même ordinateur que la simulation.

## Vue MVP

- grande zone vidéo ;
- carte simple avec position et trajet du drone ;
- statut : mission, lien simulé, batterie simulée ;
- liste d'observations avec heure et image ;
- commandes limitées : pause/maintien, reprendre, atterrir en simulation ;
- bouton « signaler personne potentielle » et bouton « signaler danger ».

Commencer par RViz2/rqt si cela permet d'intégrer plus vite. Une interface web est une amélioration de démonstration, pas une condition pour valider les modules ROS 2. Les commandes web passent toujours par ROS 2, le gestionnaire de mission et le contrôle de sécurité.
