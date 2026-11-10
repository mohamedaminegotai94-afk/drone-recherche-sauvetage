# Contrats d'interface ROS 2 — proposition initiale

Les noms ci-dessous sont des conventions de départ. Les adapter à l'intégration Gazebo/PX4 choisie, puis les garder stables pour que les deux parties puissent travailler en parallèle.

| Topic logique | Type indicatif | Producteur → consommateur | Usage |
|---|---|---|---|
| `/camera/image_raw` | `sensor_msgs/msg/Image` ou image compressée | Gazebo → perception/affichage | Vidéo RGB |
| `/camera/depth/image_raw` | `sensor_msgs/msg/Image` | Gazebo → localisation/sécurité | Distance par pixel |
| `/drone/odom` | `nav_msgs/msg/Odometry` | simulation/localisation → carte, mission | Pose et vitesse estimées |
| `/map` | `nav_msgs/msg/OccupancyGrid` | cartographie → écran/planificateur | Cellules libres, occupées, inconnues, si une carte est intégrée |
| `/victims/detections` | `vision_msgs/msg/Detection2DArray` | perception → écran/localisation | Boîtes et scores dans l'image |
| `/mission/status` | message simple ou message projet | mission → écran | État et progression |
| `/mission/command` | action/service/message contrôlé | écran → mission | Pause, continuer, point de passage, atterrir |

La pose de victime devrait à terme inclure au minimum un identifiant, une pose dans le repère de la carte, un score de confiance et un indicateur de confirmation par l'opérateur. Ne pas confondre une boîte dans l'image avec des coordonnées 3D.

## Règle de sécurité d'interface

Les commandes de l'écran passent par le gestionnaire de mission et le contrôle de sécurité. Elles ne publient pas directement des commandes moteur. Les noms exacts des topics PX4 dépendent de la version et du pont choisis.
