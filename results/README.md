# Journal des observations

Ce dossier commence sans résultat d'expérience. Le fichier CSV est un **modèle vide**, pas un constat d'absence de réponse. La préparation du dépôt et les vérifications locales ne sont pas des observations participantes.

- [REGISTRATION.md](REGISTRATION.md) fixe la référence du protocole avant le début de la fenêtre.
- [journal-template.csv](journal-template.csv) fournit les colonnes à recopier dans un futur `journal.csv`.

Pour chaque observation, appliquer les catégories et priorités de [PROTOCOL.md](../PROTOCOL.md). Enregistrer les dates en UTC ISO 8601 ; mettre entre guillemets les valeurs CSV contenant une virgule, un guillemet ou un saut de ligne, en doublant les guillemets internes. Conserver comme texte les valeurs qui commencent par `=`, `+`, `-` ou `@` si le CSV est ouvert dans un tableur.

Une copie du corps observé peut être ajoutée sous `snapshots/issue-<numero>-<horodatage>.txt`, en UTF-8 sans BOM, avec son empreinte SHA-256 dans le journal. Copier le texte exact, sans normaliser les retours à la ligne. `title_observed` conserve le titre examiné. Garder chaque première observation ; ajouter une nouvelle ligne pour toute correction analytique en citant la ligne remplacée dans `notes`.

Ne consigner que le texte volontairement publié et les métadonnées publiques nécessaires. Ne jamais exécuter un corps de réponse, ouvrir automatiquement ses liens, télécharger ses pièces jointes ou copier des données sensibles. Si le contenu doit être expurgé, le signaler et classer les éléments devenus invérifiables en conséquence.

Au bilan, indiquer l'heure d'examen, les pages parcourues, l'inclusion des Issues fermées, les suppressions ou données inaccessibles connues, puis les totaux par catégorie. Avant cet examen, utiliser « non examiné » et ne pas inventer de zéro. Ce dépôt ne programme aucune surveillance ni relance automatique.
