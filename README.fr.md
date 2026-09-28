# Hairstyle Try-on · Essai virtuel de coiffures

[English](README.md) | [简体中文](README.zh-CN.md) | [Español](README.es.md) | Français | [Português](README.pt.md) | [Русский](README.ru.md) | [한국어](README.ko.md) | [日本語](README.ja.md)

Une skill Codex pour obtenir des recommandations de coiffures réalistes et les essayer virtuellement à partir d’un selfie.

Fournissez un selfie et, si vous le souhaitez, une image de la coiffure visée. Codex recommande 4–6 propositions complètes selon les caractéristiques de vos cheveux et votre routine quotidienne. Une fois vos préférées sélectionnées, imagegen intégré génère une photo d’essai pour chaque proposition, accompagnée d’une page comparative et d’une fiche en langage courant à partager avec votre coiffeur ou coiffeuse.

## Déroulement

1. Fournissez un selfie net, de face. Les photos de profil, de l’arrière de la tête et de la coiffure souhaitée sont facultatives.
2. Choisissez les options décrivant vos cheveux, votre accord pour une permanente ou une coloration, le temps consacré au coiffage et ce que vous souhaitez éviter. Vous pouvez aussi répondre « Je ne sais pas » ou vous exprimer librement.
3. Consultez les propositions avec des images de référence, les raisons de la recommandation, les conditions nécessaires à leur réalisation et les liens vers les sources.
4. Sélectionnez 1–3 propositions par défaut, avec une photo générée pour chacune. Vous pouvez en demander davantage explicitement.
5. Examinez les photos individuelles et la comparaison côte à côte, puis demandez des ajustements en indiquant l’identifiant de la proposition.

Les coiffures sont classées par longueur et caractéristiques, pour tous les genres. Une coiffure de référence est adaptée aux conditions de vos propres cheveux. Chaque génération utilise votre selfie d’origine comme référence de votre apparence.

## Prérequis

Ce dépôt contient les instructions d’une skill, et non un modèle d’images, un service d’API ou l’implémentation d’un plugin. Il nécessite un environnement Codex capable d’utiliser des skills locales, de consulter des images et d’appeler imagegen intégré.

| Outil | Utilité | En cas d’indisponibilité |
| --- | --- | --- |
| imagegen intégré à Codex | Générer et modifier les photos d’essai | Conserver les propositions et expliquer la limite ; ne jamais basculer automatiquement vers une API payante |
| Exa (facultatif) | Outil privilégié pour rechercher et consulter des sources sur les coiffures | Utiliser une recherche web classique |
| TypeSafe (facultatif) | Filtrer et classer les descriptions des propositions | Codex effectue la sélection |
| Interactive Form Save (facultatif) | Recueillir les préférences et les choix multiples, puis relire les réponses soumises | Utiliser des choix numérotés et des réponses libres |

Le fonctionnement avec imagegen intégré ne nécessite pas de configurer `OPENAI_API_KEY`. La disponibilité, les quotas et les conditions d’utilisation des outils externes dépendent de leurs services respectifs ; ce dépôt ne donne pas accès à ces services.

## Installation

Clonez ou décompressez ce dépôt dans un dossier `hairstyle-tryon`, placé dans le répertoire de skills configuré pour votre Codex :

```text
votre-repertoire-de-skills/
└── hairstyle-tryon/
    ├── SKILL.md
    ├── README.md
    ├── README.zh-CN.md
    ├── README.es.md
    ├── README.fr.md
    ├── README.pt.md
    ├── README.ru.md
    ├── README.ko.md
    ├── README.ja.md
    └── LICENSE
```

Si `CODEX_HOME` est défini, vous pouvez utiliser son sous-répertoire `skills`. Avant l’installation, vérifiez si un dossier du même nom existe déjà et préservez vos modifications locales. Évitez d’imbriquer les fichiers dans deux dossiers `hairstyle-tryon` successifs.

## Utilisation

Appelez la skill dans Codex et joignez votre photo. Par exemple :

```text
Utilise $hairstyle-tryon pour m’aider à trouver une coiffure pour aller travailler.
Je veux garder ma couleur actuelle, sans permanente, avec environ 5 minutes de coiffage par jour.
Je vais joindre un selfie de face. Laisse-moi choisir plusieurs propositions avant de générer les photos d’essai.
```

Si vous avez une image de la coiffure souhaitée, joignez-la également et précisez les caractéristiques que vous tenez à conserver. Vous pouvez ensuite demander : « Raccourcis légèrement la frange de H02 et garde le reste inchangé. »

## Livrables

Par défaut, les résultats sont enregistrés dans `output/hairstyle-tryon/<identifiant-unique-de-session>/` au sein de l’espace de travail de la tâche. Vous pouvez choisir un autre répertoire.

- Une photo d’essai par proposition, nommée selon son identifiant et sa version.
- `comparison.html` : une page de comparaison côte à côte qui référence la photo d’origine et les images générées.
- `notes.md` : les sources, les consignes de génération, les résultats de la vérification et une fiche pour chaque coiffure.

La fiche de coiffure est une note simple à montrer en salon : les caractéristiques à conserver, les changements acceptés, votre routine de coiffage et les points à évaluer sur place. Ce n’est ni une prescription technique de coupe ni une garantie du résultat.

## Validation et utilisation des images

La version actuelle de la skill est `v0.1.0`. Les vérifications de structure ont réussi ; la génération d’images de bout en bout avec un vrai selfie n’a pas encore été validée. Les images générées servent de références visuelles. La faisabilité d’une coupe dépend d’une évaluation de vos cheveux en personne. La préservation de votre apparence repose sur les contraintes des consignes de génération et sur une vérification visuelle, sans garantie de conservation à l’identique au pixel près.

Le dépôt contient uniquement la skill et sa documentation, sans selfies d’utilisateurs ni images de référence de tiers. Les photos fournies pendant une session ne sont utilisées que pour cette demande. Avant de publier vos modifications, vérifiez les fichiers préparés pour le commit afin d’éviter d’inclure des photos, des résultats générés ou des identifiants d’accès. Les dossiers de sortie et les dossiers locaux d’entrée courants sont exclus par `.gitignore`.

## Licence

Les instructions de la skill et la documentation sont distribuées sous [licence MIT](LICENSE). Le texte standard est disponible auprès de l’[Open Source Initiative](https://opensource.org/license/mit). Cette licence n’accorde aucun droit supplémentaire sur les photos des utilisateurs, les images de référence en ligne ou les services externes.
