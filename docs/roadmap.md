# Feuille de route indicative — 16 semaines

| Semaines | Travail | Critère de sortie |
|---|---|---|
| 1–2 | Choisir et figer une combinaison compatible Gazebo/PX4/ROS 2 ; organiser le dépôt ; lancer une simulation de base. | Le drone apparaît dans la simulation et les commandes de base fonctionnent. |
| 3–4 | Construire un bâtiment simple ; ajouter caméra et télémétrie ; documenter le lancement. | Le drone se déplace dans le bâtiment et publie ses images/sa pose. |
| 5–6 | Afficher vidéo, position et statut ; séparer les tâches du binôme avec les interfaces convenues. | Premier écran utilisable avec flux et position. |
| 7–8 | Ajouter le signalement manuel d'une personne/d'un danger et sauvegarder les données d'un épisode. | MVP de base démontrable de bout en bout. |
| 9–10 | Ajouter la détection de personnes et, si possible, leur position approximative par profondeur. | Des observations sont affichées et journalisées. |
| 11–12 | Ajouter une sécurité simple et une méthode de navigation de référence. | Le drone évite ou interrompt les déplacements dangereux dans les scénarios de base. |
| 13–14 | PPO/VARE en choisissant des points de passage ; comparaison avec la référence. | Résultats comparatifs sur plusieurs cartes simulées. |
| 15–16 | Répéter les essais, analyser les métriques, préparer rapport et démonstration. | Résultats reproductibles et limites clairement présentées. |

## Priorités si le calendrier glisse

1. Garder la simulation, la vidéo, la position et le signalement manuel.
2. Utiliser un détecteur pré-entraîné au lieu d'entraîner un grand modèle.
3. Réduire le nombre de scénarios.
4. Préserver au moins une comparaison mesurée ; ne pas remplacer les résultats par une vidéo seule.
5. Présenter PPO/VARE comme extension non terminée si son intégration n'est pas fiable.
