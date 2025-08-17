# Plan de Tests - SignalPro v1.0.0

**Repository :** https://github.com/Zelprog/SignalPro-TV

## Tests de Validation v1.0.0-rc1

### 1. Tests de Compilation
- [ ] Importer indicator.pine dans TradingView Pine Editor
- [ ] Vérifier compilation sans erreurs Pine Script v5
- [ ] Confirmer affichage de tous les plots (EMA200, EMA20, Supertrend, Donchian)
- [ ] Tester table statistiques en temps réel
- [ ] Vérifier référence GitHub dans table stats

### 2. Tests Visuels - BTCUSDT 15m
**Configuration de test :**
- Symbole : BINANCE:BTCUSDT
- Timeframe : 15 minutes  
- Période : 7 derniers jours
- Paramètres : valeurs par défaut (voir parameters.pine)

**Points de vérification :**
- [ ] EMA200 et EMA20 s'affichent correctement
- [ ] Supertrend change de couleur selon la tendance (vert/rouge)
- [ ] Donchian channels encadrent les prix (high/low/mid)
- [ ] Signaux BUY/SELL apparaissent aux breakouts Donchian
- [ ] Table stats affiche régime actuel (BULL/BEAR/NEUTRAL)
- [ ] Niveaux SL/TP s'affichent si activés
- [ ] Valeurs ATR, ADX, RSI cohérentes dans table

### 3. Tests Visuels - BTCUSDT 1h  
**Configuration de test :**
- Symbole : BINANCE:BTCUSDT
- Timeframe : 1 heure
- Période : 30 derniers jours
- Paramètres : valeurs par défaut

**Points de vérification :**
- [ ] Signaux moins fréquents qu'en 15m (filtrage efficace)
- [ ] Cohérence des niveaux de régime avec timeframe plus long
- [ ] ADX respecte le seuil de 25 si activé
- [ ] RSI et EMA20 influencent signaux pullback
- [ ] Performance visuelle acceptable sur 1000+ barres

### 4. Tests Fonctionnels Logique
**Scénarios à vérifier manuellement :**

#### Filtre de Régime
- [ ] BUY uniquement si close > EMA200 ET Supertrend = 1 (vert)
- [ ] SELL uniquement si close < EMA200 ET Supertrend = -1 (rouge)
- [ ] Pas de signal si régime neutre ou ADX < seuil (25)
- [ ] Changement régime met à jour table stats correctement

#### Signaux Breakout Donchian
- [ ] Signal LONG si close > donchian_high[1] en régime bull
- [ ] Signal SHORT si close < donchian_low[1] en régime bear
- [ ] Pas de signal en range serré (prix dans middle Donchian)
- [ ] Respect période lookback Donchian (20 par défaut)

#### Signaux Pullback  
- [ ] Signal LONG si close > EMA20 et RSI > 50 en régime bull
- [ ] Signal SHORT si close < EMA20 et RSI < 50 en régime bear
- [ ] Filtre ADX fonctionne pour pullbacks si activé

#### Gestion Position
- [ ] Calcul SL distance = ATR × multiplicateur (2.0 défaut)
- [ ] Calcul TP distance = SL distance × R multiple (1.5 défaut)
- [ ] Tracking position (ACTIVE/FLAT dans table)
- [ ] Reset position variables après sortie

### 5. Tests Alertes
**Vérification système d'alertes :**
- [ ] Créer alerte sur "SIGNAL LONG" 
- [ ] Créer alerte sur "SIGNAL SHORT"
- [ ] Vérifier format JSON dans message d'alerte
- [ ] Confirmer substitution variables TradingView {{ticker}}, {{close}}, {{interval}}
- [ ] Tester conformité webhook_schema.json
- [ ] Valider champs obligatoires : v, side, symbol, price, timeframe, note

### 6. Tests Paramètres
**Modifier et observer impact :**
- [ ] EMA200 : 200 → 100 (signaux plus fréquents)
- [ ] Supertrend mult : 3.0 → 5.0 (moins de changements régime)
- [ ] Donchian length : 20 → 50 (breakouts plus larges)
- [ ] ATR SL mult : 2.0 → 1.0 (stops plus serrés)
- [ ] ADX threshold : 25 → 35 (filtrage plus strict)
- [ ] Désactiver filtres (enable_breakout/pullback/adx_filter)

### 7. Tests Cross-Timeframe  
**Vérifier cohérence :**
- [ ] BTCUSDT : 15m vs 1h vs 4h (fréquence signaux décroissante)
- [ ] ETHUSDT : 15m (validation autre pair majeure)
- [ ] ADAUSDT : 1h (test altcoin plus volatile)
- [ ] Période faible volatilité vs forte volatilité

### 8. Tests Edge Cases
**Comportements limites :**
- [ ] Market gap important (weekend crypto ou news)
- [ ] Range serré prolongé (faible volatilité, ADX < 25)
- [ ] Forte tendance unidirectionnelle (test Supertrend)
- [ ] Retournement rapide de tendance (whipsaw)
- [ ] Prix extrêmes (très hauts/bas, décimales)
- [ ] Première utilisation (pas d'historique suffisant)

### 9. Tests Performance
**Vérifications techniques :**
- [ ] Pas de lag visible sur chart 15m/1h
- [ ] Table stats se met à jour en temps réel
- [ ] Plots restent stables lors zoom/pan
- [ ] Pas d'erreurs console Pine Editor
- [ ] Mémoire/CPU acceptable (indicateurs)

## Métriques de Succès v1.0.0-rc1

### Critères de Validation
1. **Compilation** : 0 erreur Pine Script v5
2. **Affichage** : Tous les plots visibles et cohérents  
3. **Signaux** : Logique respectée (pas de signal hors régime)
4. **Performance** : Pas de lag sur 1000+ barres
5. **Alertes** : JSON valide et variables substituées
6. **Documentation** : Liens GitHub fonctionnels

### Seuils Acceptables (observationnel)
- **Fréquence signaux 15m** : 1-5 par jour (BTCUSDT)
- **Fréquence signaux 1h** : 1-3 par semaine  
- **Ratio Bull/Bear** : Cohérent avec market structure
- **ADX filter efficacité** : Réduction signaux 20-30% si activé
- **False positives** : < 10% signaux en range neutre

### Métriques qualitatives
- **UX** : Interface intuitive, groupes paramètres logiques
- **Lisibilité** : Code commenté, variables explicites
- **Documentation** : README clair, Claude.md complet
- **Maintenabilité** : Structure modulaire, versioning

## Procédure de Test

### Étape 1 : Setup & Compilation
1. Cloner repository GitHub
2. Copier indicator.pine dans TradingView Pine Editor
3. Sauvegarder comme "SignalPro v1.0.0-rc1"
4. Vérifier compilation sans erreurs
5. Documenter erreurs éventuelles dans issues GitHub

### Étape 2 : Tests Visuels Basiques
1. Appliquer sur BTCUSDT 15m
2. Vérifier tous plots affichés correctement
3. Parcourir historique 7 jours
4. Noter observations dans checklist
5. Répéter sur BTCUSDT 1h, 30 jours

### Étape 3 : Tests Fonctionnels Détaillés
1. Identifier périodes de test spécifiques (bull/bear/range)
2. Vérifier manuellement logique signaux point par point
3. Confirmer cohérence filtre régime
4. Tester modifications paramètres
5. Valider cas limites et edge cases

### Étape 4 : Tests Alertes & Integration
1. Configurer alertes TradingView
2. Tester déclenchement et format JSON
3. Valider webhook_schema.json conformité
4. Simuler intégration bot (parsing)

### Étape 5 : Rapport & Issues
1. Compiler résultats dans fichier de test
2. Créer issues GitHub pour bugs identifiés
3. Prioriser TODO pour v1.0.0 finale
4. Mettre à jour Claude.md avec résultats
5. Documenter changements nécessaires

## Templates Issues GitHub

### Bug Report
```markdown
**Version :** v1.0.0-rc1
**Environnement :** TradingView Pine Editor
**Symbole/Timeframe :** BTCUSDT 15m

**Description bug :**
[Décrire le comportement observé vs attendu]

**Reproduction :**
1. Étapes pour reproduire
2. Paramètres utilisés
3. Conditions marché

**Logs/Screenshots :**
[Si applicable]

**Impact :** [Critique/Majeur/Mineur]
```

### Feature Request
```markdown
**Type :** Enhancement
**Priorité :** [v1.0.0/v1.1.0/v2.0.0]

**Description fonctionnalité :**
[Décrire la demande]

**Justification :**
[Pourquoi c'est nécessaire]

**Implémentation suggérée :**
[Si idées techniques]
```

---

**Note :** Ces tests valident la v1.0.0-rc1 (squelette fonctionnel). Les tests de backtest complet et optimisation seront ajoutés pour la v1.0.0 finale.

**Repository :** https://github.com/Zelprog/SignalPro-TV  
**Documentation :** [Claude.md](Claude.md)  
**Issues :** [GitHub Issues](https://github.com/Zelprog/SignalPro-TV/issues)
