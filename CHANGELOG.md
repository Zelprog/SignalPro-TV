# Changelog - SignalPro TV

Toutes les modifications notables de ce projet seront documentées dans ce fichier.

Le format est basé sur [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
et ce projet adhère au [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0-rc2] - 2025-08-17

### Amélioré
- **Logique Breakout Donchian raffinée** : ajout filtre volatilité ATR percentile
- **Breakout Strength** : calcul force breakout relatif à la range Donchian
- **Pullback RSI amélioré** : implémentation RSI cross-over et sortie survente/surachat
- **Paramètres avancés** : atr_filter_len, atr_percentile, breakout_strength_min, rsi_oversold/overbought
- **Filtrage intelligent** : réduction signaux en range serré via ATR percentile (60% défaut)

### Technique
- Ajout `ta.percentrank()` pour classement volatilité relative
- Calculs `breakout_strength` normalisés par range Donchian
- Logique RSI `was_oversold/overbought` + `ta.crossover/crossunder`
- Conditions `ema_pullback_bull/bear` pour confirmation retracement

### Objectif
- **Réduction faux signaux** : Éviter breakouts en range serré
- **Amélioration qualité** : Signaux avec confirmation momentum/reversion
- **Robustesse** : Filtres adaptatifs selon conditions marché

## [1.0.0-rc1] - 2025-08-17

### Ajouté
- Structure initiale du projet avec GitHub repository
- Claude.md : documentation complète du projet et spécifications
- README.md : guide utilisateur et installation
- webhook_schema.json v1.0.0 : schéma des alertes TradingView
- Squelette indicator.pine avec plots de base (Pine Script v5)
- parameters.pine : 25+ paramètres configurables avec justifications
- tests_plan.md : procédure de validation et tests
- Structure alertcondition() pour signaux BUY/SELL
- Workflow Git intégré au processus de développement

### Technique
- Compatibilité Pine Script v5 complète
- Encodage UTF-8 pour tous les fichiers
- Architecture modulaire (Régime → Entrées → Sorties → Alertes)
- Préparation backtest embarqué
- Repository GitHub public : https://github.com/Zelprog/SignalPro-TV

### Fonctionnalités implémentées
- Filtre de régime : EMA200 + Supertrend + ADX optionnel
- Entrées Breakout Donchian (logique de base)
- Entrées Pullback EMA20 + RSI (logique de base)
- Gestion SL/TP/Trailing ATR (structure paramétrée)
- Interface utilisateur groupée par sections
- Table statistiques temps réel (version basique)
- Système d'alertes JSON pour automation future

### À venir (v1.0.0)
- Gestion position avancée (tracking, trailing stop, sorties multiples)
- Calculs backtest avec fees/slippage et métriques détaillées
- Table statistiques complète (PnL, DD, PF, HR, Sharpe)
- Tests validation sur BTCUSDT 15m/1h/4h + autres pairs
- Documentation utilisateur finale avec exemples

---

## Format de version

**MAJOR.MINOR.PATCH[-PRERELEASE]**
- **MAJOR** : changements incompatibles API/comportement
- **MINOR** : nouvelles fonctionnalités compatibles  
- **PATCH** : corrections de bugs compatibles
- **PRERELEASE** : alpha, beta, rc (release candidate)

## Liens utiles

- [Repository GitHub](https://github.com/Zelprog/SignalPro-TV)
- [Documentation complète](Claude.md)
- [Plan de tests](tests_plan.md)
- [Schéma webhook](webhook_schema.json)
- [Améliorations signaux](signal_improvements.md)
