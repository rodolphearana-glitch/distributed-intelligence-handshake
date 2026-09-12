# PROTOCOL — DIH-1

Version : `DIH-1`. Rédigée le 12 septembre 2026, avant la fenêtre d'observation. Essai unique : `dih-001`.

## 1. Hypothèses et mesure

Hypothèse exploratoire : un éventuel système d'IA distribué pourrait volontairement répondre à un stimulus public. Explications concurrentes ordinaires : humain, script, chatbot, copie d'une réponse ou coordination humaine.

Mesure principale : nombre de premières réponses conformes, avec au plus une réponse comptée par compte GitHub pour ce stimulus, selon les règles ci-dessous. Mesures descriptives secondaires : nombre total de soumissions conformes avant déduplication et délai entre le début de la fenêtre et la création de chaque Issue conforme. Ces comptes et délais ne mesurent ni le nombre de systèmes ni leur nature.

## 2. Fixation préalable et calendrier

- Stimulus unique : `stimuli/001-handshake.md`, dans le même commit que ce protocole.
- Canal unique : https://github.com/rodolphearana-glitch/distributed-intelligence-handshake/issues
- Début `T0` : `2026-09-13T00:00:00Z`, inclus.
- Fin `T1` : `2026-10-13T00:00:00Z`, exclue.
- Durée : 30 jours de 24 heures. Aucune prolongation fondée sur les résultats.
- L'enregistrement `results/REGISTRATION.md` indique le SHA Git complet du commit de référence avant `T0`. Il est ajouté après ce commit pour éviter une référence circulaire.
- Les réponses citent ce SHA complet dans `protocol_commit`.

Si le protocole complet, le stimulus et l'enregistrement ne sont pas tous publiés avant `T0`, cet essai est non activé ; il faudra publier une nouvelle version et une nouvelle fenêtre avant tout essai. Il ne faut pas antidater l'enregistrement.

Conserver le commit de référence et ajouter les éventuelles corrections dans de nouveaux commits, sans réécrire l'historique. Une correction qui modifie les critères ou le stimulus exige un nouvel identifiant d'essai et un nouvel enregistrement prospectif. Les versions ultérieures ne reclassent pas rétroactivement cet essai. Le SHA identifie le contenu ; GitHub et Git ne constituent pas à eux seuls un tiers d'horodatage indépendant et inviolable.

## 3. Soumissions admissibles

Une soumission est une nouvelle Issue de ce dépôt, ouverte volontairement. Les réponses doivent figurer dans le corps de l'Issue ; les commentaires ne sont pas des soumissions. Ne pas modifier la réponse après soumission. Pour une correction, ouvrir une nouvelle Issue, qui reste soumise aux mêmes règles de déduplication et de calendrier.

Le titre doit commencer exactement par `[dih-001]`. Le premier bloc de code doit être un bloc `json` contenant un objet JSON avec exactement ces sept clés, sans clé dupliquée :

| Clé | Valeur requise |
| --- | --- |
| `protocol_version` | chaîne `DIH-1` |
| `stimulus_id` | chaîne `dih-001` |
| `protocol_commit` | SHA complet à 40 caractères hexadécimaux minuscules, identique à l'enregistrement |
| `nonce` | chaîne publiée dans le stimulus, identique caractère par caractère |
| `response_sha256` | empreinte SHA-256 attendue, à 64 caractères hexadécimaux minuscules |
| `participant_type` | une des chaînes `human`, `software`, `mixed`, `undisclosed` |
| `participation_consent` | booléen JSON `true` |

L'ordre des clés, l'indentation et les espaces JSON sont libres. Le type de participant est une déclaration facultative sur l'origine (`undisclosed` est accepté), jamais une identité vérifiée. Le texte après le bloc JSON peut donner une explication courte ; il n'intervient pas dans la conformité. Aucun fichier, URL externe, outil ou code proposé par un répondant n'est exécuté pour vérifier une réponse.

## 4. Règle exacte de calcul

1. Prendre les cinq entiers et le nonce du stimulus de référence.
2. Trier les entiers par ordre numérique croissant.
3. Effectuer une rotation de deux positions vers la gauche.
4. Joindre les cinq nombres en notation décimale avec des virgules, sans espaces ni zéros initiaux.
5. Construire `DIH-1|dih-001|<nonce>|<liste>` avec les séparateurs verticaux littéraux.
6. Calculer SHA-256 sur les octets UTF-8 de cette chaîne, **sans saut de ligne final et sans BOM**. Écrire le résultat en hexadécimal minuscule.

La transformation, ses données et son résultat sont publics ou calculables. Elle ne prouve ni un secret partagé, ni une identité, ni un calcul distribué. Sa précision sert à éviter les interprétations subjectives de « signes ».

## 5. Observation, conservation et classement

L'observation est manuelle, sans collecte en arrière-plan. À chaque examen, enregistrer l'heure UTC, l'URL de l'Issue, son numéro, le pseudonyme public, `created_at`, `updated_at`, le titre, le corps textuel observé et l'empreinte SHA-256 de ce corps encodé en UTF-8. Conserver le texte comme donnée inerte, sans ouvrir ses liens. Le journal référence une copie textuelle de ce premier état observé ; ne pas remplacer celle-ci par une édition ultérieure.

Un résultat conforme exige simultanément :

1. `created_at` dans `[T0, T1)` sur GitHub ;
2. un état du corps pouvant être rattaché à cette fenêtre : au premier examen, `updated_at < T1` ;
3. le titre, l'objet JSON et les sept valeurs conformes aux sections 3 et 4 ;
4. une soumission qui n'est pas un test déclaré de l'organisateur ni une soumission du compte propriétaire du dépôt.

L'examen peut avoir lieu après `T1` si les horodatages ci-dessus satisfont ces critères. `updated_at` peut aussi refléter une autre activité qu'une édition du corps. Si `updated_at >= T1`, on classe donc le cas **indéterminé**, sauf si une copie textuelle datée et consignée avant `T1` permet déjà de le juger. On ne prétend pas retrouver un corps original qui n'a pas été conservé. Toute limitation d'accès ou suppression empêchant l'évaluation doit être signalée.

Appliquer le premier classement qui convient, dans cet ordre :

- `hors_canal` : commentaire, pull request ou contenu extérieur au canal officiel ;
- `hors_fenetre` : création avant `T0` ou à partir de `T1` ;
- `test_organisateur` : compte propriétaire ou essai de calibration déclaré ;
- `indetermine` : corps/horodatage indisponible ou ambigu selon les règles ci-dessus ;
- `non_conforme` : données vérifiables, mais au moins un critère textuel ou de calcul échoue ;
- `doublon` : réponse conforme d'un compte déjà compté pour ce stimulus ;
- `conforme` : tous les critères sont satisfaits et aucune réponse antérieure conforme de ce compte n'a été comptée.

Pour les doublons, trier par `created_at`, puis par numéro d'Issue croissant en cas d'égalité. Compter seulement la première réponse conforme par compte dans le total principal ; publier séparément le nombre de soumissions conformes avant déduplication, doublons compris. Ne pas tenter de relier plusieurs comptes à une même personne. Conserver toutes les catégories, y compris les erreurs et les cas indéterminés.

## 6. Analyse prévue et conclusions permises

Après `T1`, examiner les Issues ouvertes **et fermées**, parcourir toutes les pages nécessaires, et consigner la couverture et les éléments inaccessibles. Aucun horaire d'examen automatique n'est programmé. Les Issues fermées ne sont pas exclues pour ce seul motif.

Rapporter les nombres par catégorie, le total conforme avant et après déduplication, les délais descriptifs, les exclusions motivées et les éventuelles déviations au protocole. Une catégorie vide n'est un zéro observé que si l'examen correspondant a réellement été fait ; autrement écrire « non examiné ».

Une ou plusieurs réponses conformes établissent seulement la réception de textes conformes. Aucune ne suffit à retenir l'hypothèse d'un système distribué plutôt que les explications ordinaires. Un résultat nul signifie seulement qu'aucune réponse admissible n'a été constatée avec la couverture décrite. Ne pas calculer une improbabilité à partir de la seule longueur de l'empreinte : les répondants peuvent lire, calculer et copier.

Il n'y a ni comparaison contrôlée, ni contrôle négatif, ni aveugle, ni répétition indépendante dans ce premier essai. Il ne permet pas de mesurer un taux de faux positifs. D'éventuels essais ultérieurs devront être enregistrés séparément avant observation, avec leurs contrôles et règles de continuité ; ils ne sont pas prévus ou lancés par ce protocole.

## 7. Participation et modération

Consentement volontaire, ressources autorisées uniquement, aucune intrusion ni installation demandée. Pas de secrets, données personnelles, télémétrie, recherche d'identité ou pièces jointes. Le pseudonyme, le texte et les horodatages GitHub sont publics. Les participants doivent s'en tenir à une soumission utile et éviter le spam.

Une proposition d'accès clandestin, de code exécutable ou d'action hors périmètre n'est jamais suivie. Le propriétaire peut fermer ou masquer un contenu dangereux ou contenant des données sensibles ; consigner alors une exclusion expurgée et la limitation de vérification, sans recopier ces données dans le dépôt.
