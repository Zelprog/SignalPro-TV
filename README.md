# SignalPro TV → Binance

**Indicateur TradingView Pine Script v5 pour signaux crypto robustes**

[![Version](https://img.shields.io/badge/version-1.0.0--rc1-blue.svg)](https://github.com/Zelprog/SignalPro-TV/releases)
[![Pine Script](https://img.shields.io/badge/Pine%20Script-v5-green.svg)](https://www.tradingview.com/pine-script-docs/)
[![License](https://img.shields.io/badge/license-Open%20Source-orange.svg)](#)

## 🎯 Vue d'ensemble

SignalPro génère des signaux d'achat/vente sur les crypto-monnaies en combinant :
- **Filtre de régime** : EMA200 + Supertrend + ADX  
- **Entrées Breakout** : Donchian Channels avec filtre de volatilité ATR
- **Entrées Pullback** : EMA20 + RSI reversion dans la tendance
- **Gestion risque** : Stop Loss et Take Profit basés ATR avec trailing stop

## 📁 Structure du projet

```
SignalPro-TV/
├── README.md              # Guide utilisateur et installation (ce fichier)
├── Claude.md              # Documentation complète et spécifications  
├── CHANGELOG.md           # Journal des versions
├── indicator.pine         # Code Pine Script v5 principal
├── parameters.pine        # Définition paramètres avec justifications
├── webhook_schema.json    # Schéma alertes pour automation future
└── tests_plan.md         # Plan de validation et tests
```

## 🚀 Installation rapide

1. **Cloner ou télécharger** :
   ```bash
   git clone https://github.com/Zelprog/SignalPro-TV.git
   ```

2. **Copier le code** : Ouvrir `indicator.pine` et copier le contenu

3. **Pine Editor** : Aller sur TradingView → Pine Editor → Nouveau script

4. **Coller & Sauvegarder** : Remplacer le code par défaut et sauvegarder

5. **Appliquer** : Ajouter à un chart BTCUSDT ou ETHUSDT

## ⚙️ Configuration recommandée

### Timeframes optimaux
- **15m** : Signaux courts, plus fréquents (day trading)
- **1h** : Signaux moyens, équilibrés (swing trading)  
- **4h** : Signaux longs, plus robustes (position trading)

### Marchés testés
- BINANCE:BTCUSDT ✅
- BINANCE:ETHUSDT ✅  
- Autres pairs spot crypto liquides

### Paramètres par défaut (sûrs)
- EMA200: 200 périodes (régime long terme)
- Supertrend: 10 périodes, mult 3.0
- Donchian: 20 périodes  
- ATR Stop Loss: 2.0x multiplicateur
- ADX seuil: 25 (filtre tendances faibles)

## 📊 Fonctionnalités v1.0.0

### ✅ Implémenté (v1.0.0-rc1)
- [x] Plots indicateurs techniques (EMA, Supertrend, Donchian)
- [x] Logique signaux basique breakout + pullback
- [x] Filtre de régime fonctionnel
- [x] Table statistiques temps réel
- [x] Système d'alertes avec format JSON
- [x] Interface paramètres groupée et documentée
- [x] Documentation complète et structure GitHub

### 🚧 En développement  
- [ ] Logique signaux avancée avec filtres ATR
- [ ] Backtest embarqué complet (PnL, drawdown, métriques)
- [ ] Gestion position avancée (trailing stop, sorties multiples)
- [ ] Position sizing adaptatif (volatility scaling)
- [ ] Tests validation multi-timeframes

## 🔔 Alertes et Automation

Le système d'alertes génère des messages JSON compatibles automation :

```json
{
  "v": "1.0.0",
  "side": "BUY",
  "symbol": "BTCUSDT", 
  "price": "45250.75",
  "timeframe": "15m",
  "note": "DonchianBreakout+ATR"
}
```

**Schéma complet** : Voir `webhook_schema.json` pour format détaillé

**Intégration future** : webhook TradingView → bot Binance API (v2.0.0)

## 📈 Performance attendue

**Métriques cibles (indicatif) :**
- Win Rate: 45-55% (avec R:R > 1:1.5)
- Max Drawdown: < 15% 
- Profit Factor: > 1.3
- Fréquence: 1-5 signaux/semaine (1h)

**⚠️ Disclaimer :** Pas de garantie de performance. Utilisez en simulation avant trading réel.

## 🛠️ Développement

### Prérequis
- Compte TradingView (gratuit pour Pine Editor)
- Connaissance de base Pine Script v5
- Compréhension risques trading crypto
- Git (optionnel, pour contribuer)

### Workflow de développement
1. **Lire documentation** : `Claude.md` (source de vérité)
2. **Modifier code** : `indicator.pine` avec tests
3. **Tester** : BTCUSDT 15m/1h sur TradingView
4. **Documenter** : Mettre à jour `CHANGELOG.md`
5. **Partager** : Pull request ou issue GitHub

### Tests
Voir `tests_plan.md` pour procédure complète de validation.

## 🤝 Contribution

**Issues** : Bugs, suggestions d'amélioration

**Pull Requests** : Nouvelles fonctionnalités, corrections

**Documentation** : Améliorations, exemples d'usage

**Tests** : Validation sur nouvelles pairs/timeframes

## 📋 Roadmap

- **v1.0.0** : Backtest complet + validation multi-timeframes
- **v1.1.0** : Position sizing + Multi-timeframe filter  
- **v1.2.0** : Optimisations performance + nouveaux indicateurs
- **v2.0.0** : Automation Binance API + bot trading

## 📄 License & Mentions

**Usage :** Projet open source à des fins éducatives  
**Responsabilité :** Aucune garantie, utilisez à vos risques  
**Support :** Via GitHub issues et documentation  
**Auteur :** [Zelprog](https://github.com/Zelprog)

---

**Version actuelle :** v1.0.0-rc1 (Release Candidate)  
**Statut :** Squelette fonctionnel, en développement actif  
**Prochaine release :** v1.0.0 avec backtest complet

**⭐ Star ce repo si utile • 🐛 Reportez les bugs via Issues • 🚀 Contribuez via Pull Requests**
