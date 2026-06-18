# Docker Message Action

Cette action Composite génère et affiche un message d'aurevoir.

## Inputs

| Nom          | Description                | Obligatoire | Valeur par défaut  |
|--------------|----------------------------|-------------|--------------------|
| who-to-greet | Personne à saluer          | Oui         | World              |

## Outputs

| Nom             | Description                             |
|-----------------|-----------------------------------------|
| random-number   | Un nombre aléatoire généré par l'action |

## Exemple d'utilisation

\```yaml
name: Exemple de workflow
on: [push]
jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - uses: actions/checkout@v4
      - id: foo
        # Exécution locale (même dépôt) pour valider rapidement l'action
        uses: ./
        # Variante pédagogique : référencer l'action distante versionnée
        # uses: <OWNER>/<REPO>@<TAG_OU_SHA>
        with:
          who-to-greet: 'Mona the Octocat'
      - run: echo random-number "$RANDOM_NUMBER"
        shell: bash
        env:
          RANDOM_NUMBER: ${{ steps.foo.outputs.random-number }}
\```