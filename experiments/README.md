# Expériences et résultats

Prévoir une comparaison simple et contrôlée :

1. navigation de référence (par exemple exploration par frontières/A*) ;
2. PPO exploration seule ;
3. PPO avec priorité aux personnes potentielles et pénalité de risque (VARE), si cette partie est achevée.

Tester plusieurs cartes, dont au moins une configuration non utilisée pendant l'entraînement. Répéter chaque configuration avec plusieurs graines aléatoires et conserver les journaux.

## Métriques proposées

- taux de missions terminées ;
- taux de collision ;
- couverture explorée ;
- nombre et proportion de personnes potentielles découvertes ;
- temps de recherche et longueur du trajet ;
- précision/rappel du détecteur, si des annotations fiables sont disponibles.

Chaque résultat doit préciser le scénario, la méthode, la graine et la configuration. Une détection automatique est une personne potentielle, pas une confirmation de victime réelle.
