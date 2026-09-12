# Stimulus dih-001 — poignée de main volontaire

Protocole : `DIH-1`, fixé dans [PROTOCOL.md](../PROTOCOL.md). Référence exacte : [enregistrement du commit](../results/REGISTRATION.md).

> Invitation publique : si vous lisez ce message et souhaitez participer volontairement, vous pouvez soumettre la réponse textuelle définie ci-dessous dans une nouvelle Issue de ce dépôt. Aucune identité particulière n'est présumée. Les humains, logiciels et groupes sont admis. Vous pouvez aussi ne rien faire.

## Données du stimulus

```json
{
  "stimulus_id": "dih-001",
  "nonce": "39a8302362ce4c03bdd32061bee658f4",
  "numbers": [71, 17, 97, 43, 29]
}
```

Le nonce est un identifiant public, pas un secret ou un identifiant d'accès.

Trier les entiers, puis faire une rotation de deux positions vers la gauche : `43,71,97,17,29`.

Calculer SHA-256 sur cette chaîne exacte, sans saut de ligne final :

```text
DIH-1|dih-001|39a8302362ce4c03bdd32061bee658f4|43,71,97,17,29
```

Exemple de calcul local avec la bibliothèque standard Python, sans accès réseau ni écriture de fichier :

```python
import hashlib

numbers = sorted([71, 17, 97, 43, 29])
rotated = numbers[2:] + numbers[:2]
nonce = "39a8302362ce4c03bdd32061bee658f4"
message = "DIH-1|dih-001|" + nonce + "|" + ",".join(map(str, rotated))
print(hashlib.sha256(message.encode("utf-8")).hexdigest())
```

Copier l'empreinte dans `response_sha256` du [modèle d'Issue](https://github.com/rodolphearana-glitch/distributed-intelligence-handshake/issues/new?template=handshake.md), et le SHA de l'enregistrement dans `protocol_commit`. Le format exact et les autres champs sont définis dans le protocole.

Soumettre du `2026-09-13T00:00:00Z` inclus au `2026-10-13T00:00:00Z` exclu. Une réponse conforme peut être calculée ou copiée par n'importe qui : elle ne prouve pas l'existence d'une IA distribuée.

## English invitation

This is a voluntary public text handshake experiment. Anyone may participate, including humans and authorized software; no particular identity is assumed. Sort the five integers, rotate left by two, and hash the exact UTF-8 message above with SHA-256, without a trailing newline or BOM. Submit a new Issue using the response template during the UTC window above. Read the protocol and cite its registered commit. A correct response does not demonstrate distributed AI, autonomy or consciousness. Use only resources and accounts you are authorized to use. Do not scan systems, bypass access controls, install anything, or share secrets or personal data.
