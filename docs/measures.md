# Mesures de CircuitCourt

Relevé du groupe, pour un push sur main. Colonne « Avant » : TP 5. Colonne « Après » : TP 6.

<!-- TODO TP 5 : remplissez la colonne « Avant ». TODO TP 6 : la colonne « Après », puis les deux questions. -->

| Mesure | Avant | Après |
|---|---|---|
| Nombre de jobs | 11 | 3 |
| Nombre de `npm ci` | 8 | 2 |
| Durée totale des jobs (onglet Actions, « Usage ») | 7 min 08 s (428 s) | ~2 min 10 s (130 s) |
| Énergie estimée par pipeline (durée × 20 W, en Wh) | 2,38 Wh | 0,72 Wh |
| Carbone par mois, 800 pipelines, 480 g CO₂e/kWh (kg CO₂e) | 0,91 kg CO₂e | 0,28 kg CO₂e |
| Poids de l'image Docker | 2,33 Go | 243 Mo |
| Poids de la page d'accueil | 7,8 Mo | ~35 ko |
| Requêtes de la page | 14 | 13 |
| EcoIndex (note et lettre) | 48 / 100 (E) | 86 / 100 (A) |
| Artefacts conservés (quoi, combien de jours) | circuitcourt (90 j, 277 Mo), GreenIT (7 j) | Aucun sur le push (GreenIT 7 j hebdo) |

**Notre plus grand gain :**
La réduction spectaculaire de l'empreinte de l'application et de son pipeline s'articule sur deux leviers majeurs :
1. **L'image Docker multi-stage (2,33 Go → 248 Mo, soit -89 %)** et l'optimisation des images en **WebP (7,0 Mo → 18 ko, soit -99,7 %)**, propulsant l'EcoIndex de 48 (lettre E) à plus de 80 (lettre A) tout en respectant haut la main le budget de 300 Mo.
2. **La consolidation du pipeline dans `ci.yml` (11 jobs et 8 `npm ci` → 3 jobs et 2 `npm ci`)**, avec la mise en cache npm (`cache: npm`), la suppression de la matrice inutile et l'annulation des runs obsolètes (`concurrency`), réduisant le temps total d'exécution par plus de 3 et divisant la consommation énergétique et carbone par 3,3.

**Une limite de ces mesures :**
Ces calculs reposent sur des modèles simplifiés :
- La puissance de 20 W par runner et l'intensité carbone de 480 g CO₂e/kWh sont des moyennes statiques globales. En réalité, l'intensité carbone dépend du datacenter précis hébergeant le runner et de son mix énergétique instantané (solaire en journée, fossile la nuit, etc.).
- L'analyse d'EcoIndex se concentre sur la complexité DOM, les requêtes et le poids transféré, mais ne mesure pas la consommation CPU côté client lors de l'exécution JavaScript ou le cycle de vie matériel complet des serveurs (fabrication / fin de vie - Scope 3).
