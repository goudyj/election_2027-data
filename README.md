# Données de l'app Élection 2027

Toutes les données affichées par l'app (candidats, questions, sondages, calendrier, sources d'actualité) sont publiées ici. L'app les télécharge au lancement : **modifier un fichier et le pousser sur `main` suffit**, sans recompiler l'app ni passer par les stores.

## Fichiers (`v1/`)

| Fichier | Contenu |
| --- | --- |
| `candidates.json` | Candidats : identité, couleur, programme (points clés sourcés) et positions sur chaque question (-2 à 2) |
| `questions.json` | Banque de questions du questionnaire, avec leur contexte (résumé, pour, contre) |
| `polls.json` | Sondages du premier et du second tour |
| `calendar.json` | Dates clés de la campagne |
| `news.json` | Flux RSS de l'onglet Actualités et noms cherchés pour repérer chaque candidat dans les articles |

Les identifiants (`id`) relient les fichiers entre eux : les positions d'un candidat sont indexées par l'`id` des questions, et les sondages par l'`id` des candidats (ou par `otherCandidates` pour ceux absents du questionnaire).

## Mettre à jour

1. Modifier le JSON, puis mettre à jour son `updatedAt`.
2. Pousser sur `main`. La GitHub Action vérifie la syntaxe et les champs principaux.
3. L'app récupère la nouvelle version au lancement suivant, ou au retour dans l'app après 15 minutes. GitHub met jusqu'à 5 minutes à servir la nouvelle version.

Garde-fous côté app : un fichier injoignable ou mal formé est ignoré, et l'app garde la dernière version valide reçue (ou celle embarquée au build). Un id de question qui disparaît est simplement retiré des sessions en cours.

## Changer le format

`v1/` correspond au format lu par les versions de l'app déjà installées. Pour un changement incompatible (champ renommé, structure modifiée), créer `v2/`, faire pointer la nouvelle version de l'app dessus, et continuer à maintenir `v1/` tant que d'anciennes versions sont en circulation. Ajouter un champ optionnel ne nécessite pas de nouvelle version.
