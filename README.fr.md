# Blueprint Lumières automatiques

Allume et éteint automatiquement des lumières en fonction de capteurs binaires (capteurs de mouvement, capteurs d'ouverture, etc.), avec un interrupteur de contrôle optionnel pour activer ou désactiver l'automatisation.

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
| **Délai d'extinction** | Temps en secondes à attendre avant d'éteindre les lumières après que tous les capteurs sont devenus inactifs | Non | 120 |
| **Interrupteur de contrôle** | Un `input_boolean` pour activer/désactiver l'automatisation | Non | — |

## Fonctionnement

1. Quand un capteur sélectionné devient actif (mouvement détecté, porte ouverte, etc.), les lumières s'allument.
2. Quand tous les capteurs deviennent inactifs, le blueprint attend le délai configuré avant d'éteindre les lumières.
3. Si un capteur redevient actif pendant le délai, le minuteur se réinitialise et les lumières restent allumées.
4. Si un **interrupteur de contrôle** est configuré :
   - Quand l'interrupteur est **activé**, l'automatisation fonctionne normalement.
   - Quand l'interrupteur est **désactivé**, l'automatisation cesse de répondre aux capteurs.
   - Quand l'interrupteur est **réactivé**, l'automatisation reprend immédiatement : si un capteur est actuellement actif, les lumières s'allument.

## Limitations connues

- Le délai d'extinction s'applique de manière identique à tous les types de capteurs. Si vous mélangez des capteurs de mouvement (où un délai est utile) et des capteurs d'ouverture (où une extinction immédiate peut être préférable), vous devrez peut-être créer des automatisations séparées.
