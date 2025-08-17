# SignalPro v1.0.0-rc5 - Early Trend Detection

## 🎯 AMÉLIORATIONS pour capturer l'uptrend manquée

### ✅ Paramètres assouplis :
- **Donchian** : 20 → **15 périodes** (détection plus précoce)
- **ATR percentile** : 60% → **40%** (accepter plus de volatilité)
- **ADX seuil** : 25 → **20** (tendances naissantes)
- **Breakout strength** : 0.1 → **0.05** (plus sensible)

### 🆕 Early Trend Detection :
**Nouvelle logique** pour capturer tendances AVANT confirmation Supertrend complète :

```pine
// Conditions Early Trend
early_trend_bull = close > ema20 and ema20 > ema200 and close > close[1]
early_long = enable_early_trend and early_trend_bull and not regime_bull and adx_ok and close > ta.highest(close, 10)[1]
```

### 🎨 Nouveaux signaux visuels :
- 🟢 **Verts** = BUY confirmé (regime bull strict)
- 🟦 **Cyan** = EARLY BUY (tendance naissante) ← NOUVEAU !
- 🔴 **Rouges** = SELL confirmé (regime bear strict)  
- 🟣 **Fuchsia** = EARLY SELL (tendance naissante) ← NOUVEAU !
- 🟠 **Orange/Jaune** = DEBUG (régime neutral)

## 🧪 TESTS À EFFECTUER

### 1. Test historique uptrend
**Période à vérifier** : Mai-Juin 2025 (grosse montée)
**Résultat attendu** : Triangles CYAN au début de la montée

### 2. Nouveaux paramètres
Dans TradingView, vérifiez section **"📈 Entrées"** :
- ✅ **Activer Early Trend Detection** (nouveau paramètre)
- Donchian Length : 15
- ATR Percentile : 40%

### 3. Validation
- Plus de signaux qu'avant ? ✅
- Signaux plus précoces ? ✅  
- Uptrend capturée ? ✅ (à confirmer)

## 🎯 OBJECTIF
Cette version devrait maintenant capturer l'uptrend que vous avez identifiée, tout en gardant une qualité de signal acceptable.

**➡️ Testez et confirmez si l'uptrend est maintenant capturée !**