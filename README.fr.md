# Blueprint Lumières automatiques

Allume et éteint automatiquement des lumières en fonction de capteurs binaires (capteurs de mouvement, capteurs d'ouverture, etc.), avec des conditions d'éclairage et des interrupteurs de contrôle optionnels.

[Read in English](README.md)

## Installation

[![Ouvrez votre instance Home Assistant et affichez la boîte de dialogue d'importation de blueprint.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fnicolinuxfr%2Fauto-lights-blueprint%2Fgh-pages%2Ffr%2Fauto_lights.yaml)

Ou copiez cette URL manuellement :

```
https://raw.githubusercontent.com/nicolinuxfr/auto-lights-blueprint/gh-pages/fr/auto_lights.yaml
```

## Configuration

| Paramètre | Description | Requis | Défaut |
|-----------|-------------|--------|--------|
| **Lumières** | Les lumières à contrôler automatiquement | Oui | — |
| **Capteurs** | Capteurs binaires qui déclenchent les lumières (mouvement, ouverture de porte/fenêtre, etc.) | Oui | — |
| **Délai d'extinction** | Temps à attendre avant d'éteindre les lumières après qu'un capteur est devenu inactif | Non | 00:02:00 |

### Conditions d'éclairage

| Paramètre | Description | Défaut |
|-----------|-------------|--------|
| **Uniquement la nuit** | N'allume les lumières que lorsque le soleil est couché | Désactivé |
| **Capteurs de luminosité** | Capteurs d'éclairement à vérifier avant l'allumage (moyenne si plusieurs) | — |
| **Seuil de luminosité** | Les lumières ne s'allument que si la luminosité moyenne est inférieure à cette valeur | 30 lx |

### Paramètres avancés

| Paramètre | Description | Défaut |
|-----------|-------------|--------|
| **Maintenir avec portes ouvertes** | Les capteurs de porte/fenêtre ouverts empêchent l'extinction | Désactivé |
| **Interrupteurs de contrôle** | Des `input_boolean` qui activent/désactivent l'automatisation (tous doivent être activés) | — |

## Fonctionnement

1. Quand un capteur sélectionné devient actif (mouvement détecté, porte ouverte, etc.), les lumières s'allument.
2. Quand tous les capteurs deviennent inactifs, le blueprint attend le délai configuré avant d'éteindre les lumières.
3. Si un capteur redevient actif pendant le délai, le minuteur se réinitialise et les lumières restent allumées.
4. Par défaut, les capteurs de porte/fenêtre restés ouverts n'empêchent pas l'extinction — seuls les capteurs de mouvement/présence sont vérifiés.

### Conditions d'éclairage

Les conditions d'éclairage n'affectent que l'**allumage** des lumières. L'extinction fonctionne toujours, indépendamment du soleil ou de la luminosité.

- **Uniquement la nuit** : les lumières ne s'allument que quand le soleil est couché, en utilisant l'entité `sun.sun` intégrée à Home Assistant.
- **Capteurs de luminosité + seuil** : les lumières ne s'allument que si la luminosité moyenne est inférieure au seuil.
- **Les deux activés** : les lumières s'allument si **l'une ou l'autre** des conditions est remplie (nuit OU faible luminosité).
- **Aucune condition** : les lumières s'allument toujours quand un capteur se déclenche.

### Interrupteurs de contrôle

Si un ou plusieurs **interrupteurs de contrôle** sont configurés, ils doivent tous être activés pour que l'automatisation fonctionne. Quand un interrupteur est désactivé, les lumières s'éteignent après le délai configuré. Quand tous les interrupteurs sont réactivés, l'automatisation reprend immédiatement.
