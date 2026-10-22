## Langue du code et de sa documentation

### Principe général

Le français est la langue obligatoire pour les commentaires, la documentation, les messages et les noms métier produits ou modifiés par l'agent.

Les noms conventionnels du développement restent dans leur forme habituelle, en général l'anglais. Les traduire est une erreur.

Cette règle s'applique à tous les projets qui utilisent ce fichier.

### Conventions de nommage

Les noms métier créés dans le code sont en français :

- **Variables :** noms français en `snake_case`.
- **Fonctions :** noms français en `snake_case`.
- **Méthodes :** noms français en `snake_case`.
- **Classes :** noms français en `PascalCase`.
- **Constantes :** noms français en `MAJUSCULES_AVEC_UNDERSCORES`.
- **Modules Python :** noms français en `snake_case`.

Les noms doivent être explicites et décrire clairement leur fonction.

Les identifiants ne portent pas d'accent. Les accents restent dans les commentaires, les docstrings, les messages d'erreur et les textes affichés à l'utilisateur : `nombre_eleves`, pas `nombre_élèves`.

Les sigles usuels restent tels quels, en minuscules dans le `snake_case` et en majuscules dans les constantes : `id_utilisateur`, `url_api`, `response_json`, `HTTP_TIMEOUT_S`.

Le préfixe privé `_` ne se traduit pas : `_calculer_moyenne`.

Un nom déjà conventionnel en développement ne se traduit pas. La règle et les exemples sont dans « Conventions de programmation à conserver ».

### Commentaires et documentation

Tous les éléments suivants doivent être rédigés en français :

- Commentaires dans le code.
- Docstrings de module, de fonction, de méthode et de classe.
- Messages d'erreur personnalisés.
- Messages de journalisation.
- Documentation technique.
- Noms des paramètres et des variables d'exemple.
- Messages affichés à l'utilisateur.

Le corps des docstrings est en français. Les titres de sections au format Google restent en anglais, car les outils de documentation les attendent : `Args`, `Returns`, `Raises`, `Yields`, `Examples`.

Les commentaires lus par les outils ne se traduisent pas : `# noqa`, `# type: ignore`, `# pragma: no cover`.

### Exemple conforme

```python
"""Statistiques descriptives d'une classe."""

NOMBRE_MAX_TENTATIVES = 3


def calculer_statistiques_classe(id_classe: str) -> dict:
    """Calcule les statistiques descriptives d'une classe.

    Args:
        id_classe: Identifiant de la classe à analyser.

    Returns:
        Dictionnaire contenant les statistiques calculées.

    Raises:
        ValueError: Si l'identifiant de la classe est vide.
    """
    if not id_classe:
        raise ValueError("L'identifiant de la classe ne peut pas être vide.")

    # Calculer les statistiques de la classe demandée.
    statistiques = _calculer_moyennes(id_classe)

    return statistiques


def _calculer_moyennes(id_classe: str) -> dict:
    """Calcule les moyennes de la classe."""
    return {}
```

### Exceptions

Certains éléments ne peuvent pas être traduits librement :

- Les mots-clés réservés de Python, comme `def`, `class`, `return` et `if`.
- Les noms imposés par des bibliothèques externes (paramètres, méthodes, kwargs : ex. `figsize`, `inplace`, `axis`).
- Les alias conventionnels de bibliothèques : `pd`, `np`, `plt`.
- Les interfaces publiques existantes dont les noms doivent rester compatibles.
- Les noms de fichiers ou de champs définis par des formats externes.
- Les variables d'environnement, les options de CLI, les en-têtes HTTP et les clés JSON imposées par une API externe.

Dans ces situations, conserver les noms imposés par le langage, la bibliothèque, le format ou l'interface concernée.

### Code existant

Lorsqu'il modifie un fichier, l'agent n'applique cette règle qu'aux symboles qu'il crée : nom métier en français, nom conventionnel du développement laissé tel quel.

Il ne renomme pas un symbole déjà présent, public ou privé, sauf demande explicite. Un renommage non demandé casse les appelants et sort du périmètre de la modification.

### Conventions de programmation à conserver (ne pas traduire)

Un nom conventionnel en développement se garde tel quel, dans la forme utilisée par les développeurs et par la documentation du langage ou de la bibliothèque. On ne le traduit pas en français, même si le reste du fichier est en français.

La liste n'est pas exhaustive. En cas de doute, conserver la forme habituelle plutôt que d'inventer une traduction.

Vocabulaire courant à garder tel quel :

| Notion | À conserver | Ne pas écrire |
|---|---|---|
| Rôles techniques | `handler`, `callback`, `middleware`, `factory`, `adapter`, `repository`, `service`, `worker` | `gestionnaire`, `rappel`, `usine`, `adaptateur` |
| Échanges | `request`, `response`, `payload`, `client`, `session`, `token`, `header` | `requete`, `reponse`, `charge_utile`, `jeton` |
| État et exécution | `config`, `settings`, `cache`, `buffer`, `queue`, `lock`, `context`, `scope` | `configuration`, `tampon`, `file`, `verrou`, `contexte` |
| Contrôle | `timeout`, `retry`, `backoff`, `batch`, `offset`, `limit`, `cursor` | `delai`, `nouvelle_tentative`, `lot`, `decalage` |
| Données techniques | `parser`, `serializer`, `schema`, `query`, `index`, `mapping` | `analyseur`, `serialiseur`, `requete`, `correspondance` |

Noms imposés ou attendus par Python et ses outils :

| Notion | À conserver | Pourquoi |
|---|---|---|
| Point d'entrée | `main` | Convention quasi universelle (`def main`, `if __name__ == "__main__"`) |
| Module / garde d'entrée | `__main__` | Imposé par Python |
| Méthodes spéciales | `__init__`, `__str__`, `__repr__`, etc. | Imposées par Python |
| Journalisation | `logger` | Convention `logging.getLogger` |
| Arguments CLI | `argv`, `args`, `kwargs` | Convention stdlib / signatures |
| Préfixe de tests | `test_`, `Test` | Imposé / attendu par pytest et outils |
| Fixtures pytest courantes | `tmp_path`, `monkeypatch`, `capsys` | Noms fournis par pytest |
| Drapeaux CLI idiomatiques | `--skip-*`, `--dry-run`, `--help`, `--version` | Idiomes CLI répandus |
| Identifiants techniques Unix / fichiers | `mtime`, `cwd`, `stdout`, `stderr`, `stdin` | Vocabulaire système standard |
| Racine de chemin (pathlib) | `stem` (attribut Path) | API pathlib ; une variable métier peut s'appeler autrement |

Les **noms métier du projet** (classe, élève, facture, statistiques, messages utilisateur) restent en français. Un terme technique conventionnel accolé à un nom métier garde sa forme : `id_utilisateur`, `cache_facture`, `timeout_import`.

### Vérification obligatoire

Lorsqu'il crée ou modifie du code Python, l'agent doit vérifier que les nouveaux noms et la documentation respectent cette règle.

Dans sa réponse finale, il doit ajouter une section **Style de code** indiquant :

- **Règles consultées :** `style_code_python.md`.
- **Langue :** français.
- **Application :** appliquées, partiellement appliquées ou non appliquées.
- **Exceptions :** préciser les éléments conservés dans une autre langue et pourquoi.

L'agent ne doit jamais prétendre avoir vérifié le respect de ces règles sans avoir réellement examiné le code.
