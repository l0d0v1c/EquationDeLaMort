# Calculateur de Patrimoine Résiduel 📊

Une application web moderne pour estimer l'évolution du patrimoine en fonction de l'espérance de vie résiduelle, intégrant des modèles économiques avancés de rémunération du capital.

## 🎯 Objectif

Calculer le patrimoine restant selon :
- **Données démographiques INSEE 2020**
- **Modèles de rémunération du capital** selon l'inflation
- **Scénarios économiques probabilistes**
- **Prise en compte des pensions de retraite**

## 📱 Interface

Interface responsive optimisée smartphone avec :
- **Police Lexend Deca** pour une meilleure lisibilité
- **Design glassmorphism** avec animations CSS3
- **Graphiques interactifs** Chart.js avec points cliquables
- **Notifications temps réel** jQuery

## 🧮 Modèle de Simulation

### Simulation Mois par Mois

Le calcul s'effectue par **simulation mensuelle** avec deux phases distinctes :

#### **Phase AVANT la retraite** (Âge actuel → Âge de retraite)
```
Capital(mois+1) = Capital(mois) × (1 + r_mensuel) + Revenu_mensuel - Prélèvement_avant
```

#### **Phase APRÈS la retraite** (Âge de retraite → Décès)
```
Capital(mois+1) = Capital(mois) × (1 + r_mensuel) + Pension_mensuelle - Prélèvement_après
```

### Variables du Modèle

- **P** : Patrimoine initial (€)
- **r_mensuel** : Taux de rémunération mensuel effectif
- **i_mensuel** : Taux d'inflation mensuel effectif
- **NR** : Nombre d'années de vie résiduelle (INSEE 2020)
- **Revenu_mensuel** : Revenus mensuels avant la retraite (€)
- **Prélèvement_avant** : Prélèvement mensuel sur capital avant retraite (€)
- **Prélèvement_après** : Prélèvement mensuel sur capital après retraite (€)
- **Pension_mensuelle** : Pension de retraite mensuelle (€)
- **p_mensuel** : Taux de revalorisation mensuel des retraites
- **A** : Âge actuel
- **R** : Âge de départ à la retraite

### Ajustements Inflation

Tous les flux monétaires sont ajustés mensuellement :
- **Revenus** : × (1 + i_mensuel)
- **Prélèvements** : × (1 + i_mensuel) 
- **Pensions** : × (1 + p_mensuel) annuellement

## 📈 Modèles de Rémunération du Capital

### Formule Générale Composite

```
R_capital(π) = R_base + β(scénario) × π + γ × π² + δ × volatilité_π
```

Où :
- **R_base** = 3.5% (taux de rendement réel de base)
- **π** = Taux d'inflation (%)
- **γ** = -0.05 (coefficient non-linéaire)
- **δ** = -0.3 (coefficient de volatilité)

### Scénarios Économiques

#### 📈 Scénario Optimiste (β = +0.65)
- **Contexte** : Inflation modérée, politique monétaire accommodante
- **Portefeuille** : Actifs réels dominants (immobilier, matières premières)
- **Hypothèse** : Pricing power intact, adaptation à l'inflation

#### 📊 Scénario Médian (β = -0.15)
- **Contexte** : Inflation variable, politique monétaire réactive
- **Portefeuille** : Diversifié (actions, obligations, actifs réels)
- **Hypothèse** : Adaptation partielle, économie mixte

#### 📉 Scénario Pessimiste (β = -0.85)
- **Contexte** : Inflation élevée/volatile, politique restrictive
- **Portefeuille** : Obligations dominantes
- **Hypothèse** : Stagflation, compression des marges

#### 🎯 Moyenne Pondérée
Probabilités dynamiques selon le niveau d'inflation :

| Inflation | Optimiste | Médian | Pessimiste |
|-----------|-----------|--------|------------|
| 0-2% | 30% | 60% | 10% |
| 2-4% | 40% | 50% | 10% |
| 4-6% | 20% | 50% | 30% |
| 6-8% | 10% | 40% | 50% |
| >8% | 5% | 25% | 70% |

## 📊 Modèles d'Espérance de Vie

### Modèle Gompertz-Makeham (par défaut)

Utilise la **fonction de survie conditionnelle** avec paramètres ajustés TH/TF 00-02 :

```
S(t|a) = exp(-A×t - (B/ln(c))×(c^(a+t) - c^a))
```

**Paramètres par genre :**
- **Hommes** : A=0.000958199, B=0.00002900877, c=1.101995
- **Femmes** : A=0.00019153196, B=0.0000078122169, c=1.113875875

**Calcul d'espérance :** Intégration numérique de la fonction de survie avec pas mensuel.

### Modèle Linéaire (INSEE 2020)

**Hommes :** `NR = -0.9279 × Âge + 78.492`
**Femmes :** `NR = -0.9582 × Âge + 84.793`

**Note :** Le modèle Gompertz-Makeham est plus précis, particulièrement aux âges élevés.

## 🔧 Fonctionnalités

### Calculs
- ✅ **Simulation mois par mois** sur la durée de vie résiduelle
- ✅ **Double modèle d'espérance de vie** : Gompertz-Makeham (défaut) ou linéaire INSEE
- ✅ **Modèle bi-phasique** : avant/après retraite avec flux différenciés
- ✅ **Ajustement automatique** revenus/prélèvements/pensions avec inflation
- ✅ **Détection épuisement** du capital avec alerte d'âge
- ✅ **Génération tableau** annuel détaillé

### Interface
- ✅ **Validation temps réel** des champs numériques
- ✅ **Calcul automatique** du taux selon le modèle choisi
- ✅ **Graphique animé** avec interactions au clic
- ✅ **Notifications stylées** pour les détails par âge
- ✅ **Rapport HTML** détaillé avec bouton d'impression
- ✅ **URL de partage** avec paramètres intégrés
- ✅ **Mode responsive** optimisé mobile/tablette

### Modèles
- ✅ **2 modèles d'espérance de vie** : Gompertz-Makeham + linéaire INSEE
- ✅ **5 modes de rémunération** : Manuel + 4 scénarios économiques
- ✅ **Mise à jour dynamique** quand l'inflation change
- ✅ **Descriptions contextuelles** des hypothèses
- ✅ **Seuils de sécurité** pour éviter les aberrations

## 🚨 Limitations et Précautions

### Validité du Modèle
- **Espérance de vie** : Modèle Gompertz-Makeham basé sur données TH/TF 00-02
- **Rémunération capital** : Synthèse d'études sur 16 pays (1957-1996)
- **Calibrage** : Coefficients estimés par logique économique
- **Extrapolation** : Relations historiques projetées vers le futur
- **Simplification** : Relations multivariées complexes simplifiées

### Utilisation Recommandée
- ✅ **Outil de simulation** et d'analyse de scénarios
- ✅ **Cadre conceptuel** pour la planification patrimoniale
- ✅ **Support pédagogique** pour comprendre les mécanismes
- ❌ **Pas une prédiction précise** à usage professionnel
- ❌ **Pas un conseil financier** personnalisé

### Contexte d'Application
- **Géographique** : Calibré sur économies développées
- **Temporel** : Optimal pour horizons 6-24 mois
- **Révision** : Recommandée annuellement selon évolution économique

## 💻 Technologies

- **Frontend** : HTML5, CSS3, JavaScript ES6
- **Modèles mathématiques** : Gompertz-Makeham, simulation Monte Carlo
- **Animations** : Transitions CSS3, animations keyframes
- **Graphiques** : Chart.js 3.7.1 avec interactions
- **UI/UX** : jQuery 3.6.0, design glassmorphism
- **Partage** : URL encoding, paramètres persistants
- **Typographie** : Google Fonts (Lexend Deca)
- **Responsive** : Media queries, viewport mobile

## 🌐 Accès

**[Application en ligne](https://l0d0v1c.github.io/EquationDeLaMort/)**

Interface optimisée pour tous supports : desktop, tablette, smartphone.

---

*Application développée avec IA générative pour la recherche en économie comportementale et planification patrimoniale.*