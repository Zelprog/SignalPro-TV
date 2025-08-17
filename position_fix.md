# CORRECTION URGENTE - Gestion Position SignalPro

## 🐛 PROBLÈME IDENTIFIÉ
Les indicateurs sont "figés" car il n'y a pas de logique de SORTIE de position.

## 🔧 SOLUTION MINIMALE (v1.0.0-rc3)

### Code à ajouter après les conditions d'entrée :

```pine
// === GESTION SORTIES (BASIQUE) ===
// Conditions de sortie simples
exit_long_sl = in_position and close <= stop_loss
exit_long_tp = in_position and close >= take_profit1
exit_short_sl = in_position and close >= stop_loss  
exit_short_tp = in_position and close <= take_profit1

// Sortie de position
exit_position = exit_long_sl or exit_long_tp or exit_short_sl or exit_short_tp

if exit_position
    in_position := false
    entry_price := na
    stop_loss := na
    take_profit1 := na

// Signaux de sortie (optionnel pour visualisation)
plotshape(exit_long_sl, style=shape.xcross, location=location.abovebar, color=color.red, size=size.small, title="EXIT SL")
plotshape(exit_long_tp, style=shape.diamond, location=location.abovebar, color=color.green, size=size.small, title="EXIT TP")
plotshape(exit_short_sl, style=shape.xcross, location=location.belowbar, color=color.red, size=size.small, title="EXIT SL")
plotshape(exit_short_tp, style=shape.diamond, location=location.belowbar, color=color.green, size=size.small, title="EXIT TP")
```

## 🎯 RÉSULTAT ATTENDU
- ✅ Indicateurs redeviennent mobiles
- ✅ Nouveaux signaux possibles après sortie
- ✅ Points BUY/SELL + EXIT visibles
- ✅ SL/TP se mettent à jour

## 📋 ÉTAPES SUIVANTES (v1.0.0)
1. Trailing stop ATR
2. Sorties multiples (TP1, TP2)
3. Gestion position avancée
4. Backtest embarqué

---

**PRIORITÉ 1 :** Corriger le problème technique pour rendre les tests possibles.
