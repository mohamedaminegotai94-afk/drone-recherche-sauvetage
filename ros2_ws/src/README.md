# Packages ROS 2

Créer ici les packages ROS 2 du projet quand le premier vol simulé fonctionne. Proposition de découpage à confirmer :

- `rescue_drone_bringup` : lancements et paramètres ;
- `rescue_drone_perception` : caméra et détection ;
- `rescue_drone_mission` : mission, sécurité et navigation ;
- `rescue_drone_dashboard_bridge` : données destinées à l'écran ;
- `rescue_drone_interfaces` : messages propres au projet, seulement si les messages standards ne suffisent pas.

Ne pas ajouter tous les packages en même temps : commencer par un nœud qui lit la pose et un nœud qui reçoit une commande.
