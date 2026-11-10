# Architecture du système

## Périmètre

La cible est un drone éclaireur **simulé** dans un bâtiment de plain-pied. Le premier prototype privilégie la téléopération, la vidéo, la position du drone et le signalement manuel. La détection, la navigation autonome et PPO/VARE arrivent par étapes.

## Schéma des composants

```text
                    ┌─────────────────────────────┐
                    │ Gazebo                      │
                    │ bâtiment + quad + capteurs  │
                    └──────────────┬──────────────┘
                                   │ images, profondeur,
                                   │ pose et télémétrie
                                   ▼
┌──────────────────────────────────────────────────────────────┐
│ ROS 2                                                        │
│                                                              │
│ caméra ──► perception YOLO ──► localisation d'observation    │
│ pose ────► état / carte ──────────────────────────────────┐  │
│ opérateur ou PPO ──► gestion de mission ──► sécurité ─────┼──┼──► PX4 SITL
│                                                         │  │
│ vidéo + carte + état + observations ◄────────────────────┘  │
└──────────────────────────────┬───────────────────────────────┘
                               ▼
                    Écran de l'opérateur
             vidéo | carte | statut | signalements
```

PX4 SITL s'occupe de la stabilisation et de l'exécution du vol simulé. Le gestionnaire de mission envoie des consignes de haut niveau ; le module de sécurité les contrôle avant leur transmission. Le navigateur ne doit pas commander directement les moteurs.

## Modules

1. **Simulation** — Un monde Gazebo avec un bâtiment simple, des obstacles, des personnes simulées et une caméra RGB. La profondeur peut être activée pour estimer la distance aux objets.
2. **Pont de vol** — PX4 SITL et ROS 2 échangent les consignes de vol et la télémétrie en utilisant l'intégration compatible avec les versions choisies.
3. **État/localisation** — Pour la première démonstration, utiliser la pose de référence fournie par Gazebo et l'indiquer clairement. Plus tard, remplacer cette source par un package de localisation/SLAM existant si le périmètre le permet.
4. **Perception** — Un nœud reçoit l'image et produit des détections de personnes potentielles : boîte, classe et score de confiance.
5. **Localisation des observations** — Pour estimer une position dans la carte, combiner la boîte de détection, la profondeur, la pose du drone et la transformation caméra-drone. Au tout début, un clic opérateur peut simplement enregistrer la pose courante du drone comme position approximative de l'observation.
6. **Gestion de mission** — Accepte les commandes de l'opérateur. Plus tard, il pourra choisir des points d'exploration par frontières/A*, puis PPO.
7. **Sécurité** — Limite les consignes, surveille la distance aux obstacles et prévoit un arrêt/maintien/atterrissage simulé en cas de situation anormale. Garder une commande de reprise manuelle.
8. **Écran opérateur** — Affiche le flux vidéo, la carte, la position, le statut de mission et les signalements. L'écran envoie ses commandes au gestionnaire de mission, jamais directement à PX4.
9. **Journalisation** — Enregistre les épisodes et les topics utiles avec rosbag2 afin de calculer les métriques.

## Flux principal

```text
Gazebo/PX4 → caméra et pose → ROS 2 → écran opérateur
                                     ├→ détection de personnes
                                     ├→ carte et signalements
Écran opérateur → commande de mission → contrôle de sécurité → PX4 SITL → Gazebo
```

## Extension PPO / VARE

PPO sera un planificateur **de haut niveau** : il choisit le prochain point à explorer et non les commandes des moteurs. Il sera comparé à une méthode de référence (exploration par frontières avec A*). VARE peut classer les points candidats selon le gain d'exploration, les indices de victime, le risque et le coût du trajet. Il faut décider expérimentalement si ce score sert à classer les points ou à définir une partie de la récompense PPO ; éviter de mélanger les deux sans comparaison.
