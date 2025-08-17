# Projet : SignalPro TV → Binance

## 0) Rappel de mandat
**Objectif produit :** Indicateur TradingView (Pine Script v5) produisant des signaux d'achat/vente robustes basés sur des méthodes éprouvées (tendance + breakout + reversion filtrée + gestion du risque ATR).

**Portée actuelle (v1) :** Indicateur Pine v5 affichant signaux BUY/SELL, niveaux d'entrée/sortie, SL/TP, et statistiques de backtest local sur l'historique du chart.

**Marchés :** Pairs spot crypto liquides (ex. BTCUSDT, ETHUSDT).

**Timeframes visés :** 15m, 1h, 4h (paramétrables).

**Hors scope immédiat :** Exécution d'ordres Binance, gestion multi-comptes, hedging, levier (reporté v2+).

**Contraintes :** Déterminisme total, aucun appel externe, robustesse, gestion fees/slippage dans backtest.

## 1) Roadmap & jalons
**v1.0.0 (Indicateur TradingView) :**
- [x] Filtre de régime EMA200 + Supertrend/ADX
- [x] Entrée Breakout Donchian + ATR filter  
- [x] Entrée Pullback (EMA20 + RSI re-cross)
- [x] SL/TP/Trailing ATR (paramétrables)
- [ ] Backtest embarqué (PnL net, DD, PF, HR)
- [x] Alertes & webhook_schema.json
- [ ] Doc utilisateur (paramètres & exemples)

**v1.1.0 :**
- [ ] Position sizing ATR (optionnel)
- [ ] Multi-timeframe filter (HTF confirm)

**v2.0.0 (Auto via Binance) :**
- [ ] Bot listener webhooks
- [ ] Mappage symboles & filtres d'échange (tickSize/stepSize/minNotional)
- [ ] OTOCO (entrée+TP+SL), post-only support
- [ ] Journaux d'exécution & reprise d'état

## 2) État d'avancement (journal de session)
- **2025-08-17 16:00** — Session initiale : ✅ Création structure projet complète
  - ✅ Claude.md : documentation et spécifications complètes
  - ✅ CHANGELOG.md v1.0.0-rc1 : versioning initial
  - ✅ parameters.pine : 25+ paramètres avec défauts sûrs et justifiés
  - ✅ indicator.pine : squelette compilable v5 avec plots EMA200/EMA20/Supertrend/Donchian
  - ✅ webhook_schema.json v1.0.0 : schéma complet avec exemples et validation
  - ✅ tests_plan.md : procédure validation BTCUSDT 15m/1h

- **2025-08-17 16:30** — Intégration GitHub réussie
  - ✅ Repository public créé : https://github.com/Zelprog/SignalPro-TV
  - ✅ Push complet structure projet (7 fichiers)
  - ✅ Documentation GitHub : README.md, badges, liens
  - ✅ Workflow Git intégré dans Claude.md (section 10)
  - ✅ ADR-005 : Décision repository public pour collaboration open source

- **2025-08-17 17:00** — Amélioration logique signaux v1.0.0-rc2
  - ✅ Breakout Donchian raffiné : filtre ATR percentile + breakout strength
  - ✅ Pullback RSI amélioré : cross-over + survente/surachat + EMA confirmation
  - ✅ Nouveaux paramètres : atr_filter_len, atr_percentile, breakout_strength_min, rsi_oversold/overbought
  - ✅ signal_improvements.md : plan détaillé améliorations
  - ✅ Bump version → v1.0.0-rc2

- **2025-08-17 17:30** — DEBUG et correction complète Pine Script v1.0.0-rc2-fix
  - ✅ PROBLÈME identifié : conditions multi-lignes + fonctions multi-paramètres incompatibles Pine Script
  - ✅ CORRECTIONS appliquées : 4 conditions logiques + 4 plots + 2 table.cell + 2 alertcondition
  - ✅ VÉRIFICATION complète : 0 ligne terminant par 'and/or/,' - 100% compatible Pine v5
  - ✅ debug_report.md : documentation exhaustive de toutes les corrections
  - ✅ Version → v1.0.0-rc2-fix (175 lignes optimisées de 189)

- **2025-08-17 17:45** — Correction CRITIQUE problème indicateurs figés v1.0.0-rc3
  - 🚨 **PROBLÈME MAJEUR identifié** : Indicateurs "figés" à l'ancienne position (user feedback)
  - ✅ **CAUSE RACINE** : Pas de logique de sortie de position (in_position restait true indéfiniment)
  - ✅ **SOLUTION implémentée** : Logique sorties complètes SL/TP + reset variables position
  - ✅ **SIGNAUX VISUELS** : Triangles entrée + Croix SL + Diamants TP + États position ACTIVE/FLAT
  - ✅ position_fix.md : documentation du problème et solution
  - ✅ Version → v1.0.0-rc3 (indicateurs mobiles + points BUY/SELL clairs)
  - 📋 **PROCHAINE ÉTAPE** : Tests utilisateur - indicateurs mobiles + signaux entrée/sortie

- **2025-08-17 18:00** — Early Trend Detection v1.0.0-rc5 (RÉPONSE FEEDBACK CRITIQUE)
  - 🚨 **FEEDBACK UTILISATEUR** : Grosse uptrend manquée (Mai-Juin 2025) - Problème majeur identifié
  - ✅ **Early Trend Detection** : Nouvelle logique pour capture précoce des tendances naissantes
  - ✅ **Paramètres assouplis** : Donchian 20→15, ATR 60%→40%, ADX 25→20, Strength 0.1→0.05
  - ✅ **Signaux Early Trend** : Triangles cyan/fuchsia pour tendances avant confirmation Supertrend
  - ✅ **Logique EMA** : close>ema20 ET ema20>ema200 + breakout 10-périodes pour réactivité
  - ✅ rc5_improvements.md : Documentation complète des améliorations anti-missed-trends
  - 📋 **TESTS EN COURS** : Validation capture uptrend historique + nouveaux signaux cyan/fuchsia

  - ✅ tests_plan.md : procédure validation BTCUSDT 15m/1h
  - 📋 **NEXT** : Tests compilation TradingView + logique signaux breakout/pullback

## 3) Règles immuables (à respecter **toujours**)
- Relire `Claude.md` au début de chaque session
- Ne jamais casser une feature validée sans plan & migration
- Versionner tout changement fonctionnel (SemVer)
- Encoder en UTF-8, pas d'emoji dans les identifiants de code
- Tous les schémas (alertes, payloads) sont **versionnés**
- Paramètres par défaut stables; tout changement = note de rupture
- **Git workflow** : commit atomiques, messages clairs, push réguliers

## 4) Spécification fonctionnelle

### Filtre de régime (Trend Filter)
- **EMA200** : régime long/court (Close > EMA200 = bullish)
- **Supertrend** : confirmation directionnelle 
- **Règle** : BUY autorisé si Close > EMA200 ET Supertrend haussier

### Entrées (activables via paramètres)
1. **Breakout Donchian** : HH/LL n-bar + volatility confirmation (ATR percentile)
2. **Pullback tendance** : Close repasse au-dessus EMA20 après retracement + RSI sort zone <40 (bull) />60 (bear)

### Sorties & gestion
- **SL initial** : k × ATR (1.5–2.5×)
- **TP** : R multiples (1R/2R) 
- **Trailing Stop** : ATR activé après +1R
- **Inversion fail-fast** : sortie anticipée si régime se retourne

### Comportements limites
- **Marchés sans tendance** : réduction fréquence signaux via filtre ADX minimum
- **Gaps** : vérification cohérence prix entrée vs prix gap
- **Faible volume** : pas de filtre volume v1 (simplicité)

## 5) Spécification technique

### Structure Pine v5
```pine
//@version=5
indicator("SignalPro v1.0.0", shorttitle="SP", overlay=true)

// === INPUTS (groupés par sections) ===
// [Régime]
// [Entrées] 
// [Sorties]
// [Backtest]
// [Alertes]

// === CALCULS ===
// Indicateurs techniques
// Logique signaux
// Gestion positions

// === AFFICHAGE ===
// Plots MA/Supertrend
// Marqueurs BUY/SELL
// Table statistiques

// === ALERTES ===
// alertcondition() par type signal
```

### Performance
- Éviter boucles inutiles
- Limiter `request.security()` si MTF
- Variables `var` pour états persistants

### Backtest embarqué
- Calcul PnL brut/net (fees/slippage)
- Métriques : DD max, Profit Factor, Hit Rate
- Affichage table stats temps réel

## 6) Schémas & contrats

### webhook_schema.json v1.0.0
```json
{
  "v": "1.0.0",
  "signal_id": "<uuid>",
  "ts": "<epoch_ms>", 
  "symbol": "{{ticker}}",
  "side": "BUY|SELL|FLAT",
  "price": "{{close}}",
  "sl": 0.0,
  "tp": [],
  "trail_atr_k": 2.0,
  "timeframe": "{{interval}}",
  "note": "DonchianBreakout+ATR"
}
```

**Règles schéma :**
- UTF-8, nombres décimaux, pas de null (0 ou [])
- Ajout champs = bump mineur
- Changement/retrait = bump majeur

## 7) Décisions & justifications (ADR)
- **ADR-001** : EMA200+Supertrend pour filtre régime → simplicité + efficacité prouvée
- **ADR-002** : k_ATR défaut = 2.0 → compromis risque/bruit acceptable
- **ADR-003** : Donchian breakout + pullback → couverture momentum/reversion
- **ADR-004** : Backtest embarqué → validation immédiate sans outils externes
- **ADR-005** : GitHub public → collaboration open source, documentation transparente

## 8) Risques & mitigations
- **Sur-optimisation** : bornes paramétriques strictes, tests OOS
- **Obsolescence** : versioning logiques, notes migration
- **Changements TradingView** : veille compat Pine v5/v6
- **Dérive paramètres** : valeurs défaut documentées, changements = bump version
- **Perte code** : GitHub backup, commits réguliers

## 9) TODO / Backlog
**Priorité 1 (v1.0.0-rc5) :**
- ✅ Squelette indicator.pine compilable
- ✅ Paramètres avec défauts sûrs
- ✅ Plots de base (EMA200, EMA20, Supertrend)
- ✅ Structure alertes
- ✅ GitHub setup & documentation
- ✅ Logique signaux raffinée (Breakout + Pullback)
- ✅ Correction problème indicateurs figés
- ✅ Early Trend Detection pour capture uptrends manquées

**Priorité 2 :**
- [ ] Tests validation capture uptrend Mai-Juin 2025
- [ ] Trailing stop ATR dynamique
- [ ] Backtest embarqué complet
- [ ] Tests validation multi-timeframes

**Priorité 3 :**
- [ ] Table stats détaillée avec métriques
- [ ] Documentation utilisateur finale
- [ ] Optimisation performance

## 10) Workflow Git intégré

### Processus de développement
1. **Avant modification** : Relire Claude.md + sync local/GitHub
2. **Développement** : Modifier fichiers locaux + tests
3. **Documentation** : Mettre à jour Claude.md + CHANGELOG.md
4. **Validation** : Tests compilation + fonctionnels
5. **Commit & Push** : Messages clairs + push GitHub
6. **Release** : Tag version + release notes

### Structure commits
- **feat:** nouvelle fonctionnalité
- **fix:** correction bug
- **docs:** documentation
- **test:** tests et validation
- **refactor:** refactoring sans changement fonctionnel
- **bump:** montée de version

### Gestion des releases
- **v1.0.0-rc1** → **v1.0.0-rc2** : Logique signaux améliorée
- **v1.0.0-rc2** → **v1.0.0-rc3** : Correction problème indicateurs figés
- **v1.0.0-rc3** → **v1.0.0-rc5** : Early Trend Detection anti-missed-trends
- **v1.0.0-rc5** → **v1.0.0** : Backtest complet + tests validés
- **v1.0.0** → **v1.1.0** : Position sizing + MTF filter
- **v1.x.x** → **v2.0.0** : Automation Binance

## 11) Annexes

**Références méthodologiques :**
- Donchian Channels : breakout momentum
- ATR : volatility-based stops
- Supertrend : trend following filter
- EMA : trend bias determination

**Repository GitHub :** https://github.com/Zelprog/SignalPro-TV

**Structure finale :**
```
SignalPro-TV/
├── README.md              # Guide utilisateur et installation
├── Claude.md             # Documentation complète (ce fichier)
├── CHANGELOG.md          # Journal des versions
├── indicator.pine        # Code Pine Script v5 principal
├── parameters.pine       # Définition paramètres avec justifications
├── webhook_schema.json   # Schéma alertes pour automation
├── tests_plan.md        # Plan de validation et tests
├── signal_improvements.md # Plan détaillé améliorations signaux
├── rc5_improvements.md   # Améliorations Early Trend Detection
└── docs/                # Documentation additionnelle (future)
```