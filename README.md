# 🏛️ Bond Credit Valuation – Modèle complet de valorisation d’obligations avec spread de crédit ajusté au risque

---

## 🔎 Introduction

Ce projet modélise la valorisation d'obligations d'entreprises en intégrant dynamiquement le risque de crédit à travers le **spread de crédit ajusté**.  
Contrairement à une approche simplifiée par taux sans risque, ce modèle considère :

- Le **niveau de risque de l’émetteur** (via sa notation)
- Le **secteur d’activité** (via la LGD spécifique)
- Le **scénario économique** (normal, stress, recovery)

L’objectif est de construire un outil réaliste d’évaluation de titres obligataires utilisé en gestion active, en analyse de crédit ou en debt selection sur le buy-side.

---

## 🎯 Objectifs du projet

- 💡 Valoriser une obligation en actualisant ses flux futurs avec un **taux ajusté au risque de défaut**
- 🔧 Construire un **spread de crédit dynamique** basé sur la **perte attendue (EL = PD × LGD)**
- 📊 Simuler des scénarios économiques pour observer l’impact du risque sur la valeur
- 📉 Tester la sensibilité du prix de l’obligation au spread, à la notation, et au secteur
- 🧠 Fournir un support visuel et analytique aux décisions d’investissement

---

## 💼 Pourquoi ce projet est pertinent pour le buy-side

Dans un contexte de gestion active obligataire ou de private debt :
- Les spreads ne sont **pas constants** : ils dépendent du risque réel
- Les gérants ont besoin d’une **évaluation ajustée au risque crédit**
- La notation ne suffit pas : il faut **quantifier l’impact** (via EL, pricing, stress)
- Le projet simule une démarche d’**allocation rationnelle et défendable**

Ce modèle donne un aperçu **opérationnel** du travail d’un analyste crédit buy-side.

---

## 🧱 Méthodologie complète

### 1. 📑 Données utilisées

Les données d'entrée (`data/obligations.csv`) comprennent :
- Nom de l’émetteur
- Notation (ex : A, BBB, BB, etc.)
- Maturité (en années)
- Taux du coupon
- Fréquence de paiement (annuelle, semestrielle, trimestrielle)
- Secteur (Industrie, Finance, Services…)
- Montant nominal (par défaut : 1000€)
- Date d’émission (pour future extension dynamique)

---

### 2. 💰 Modélisation des flux de trésorerie

Fonction `generate_cash_flows()` :
- Calcule les paiements futurs de coupon
- Ajoute le remboursement final du nominal
- Paramétrée par la fréquence (1, 2, 4)

---

### 3. 📈 Taux d’actualisation avec spread de crédit

Taux d’actualisation = **Taux sans risque + spread de crédit**

Le **spread de crédit** est construit dynamiquement à partir de :
- `PD` (Probabilité de défaut) : dépend de la notation
- `LGD` (Loss Given Default) : dépend du secteur
- `EL = PD × LGD` → proportion de perte attendue

Cette EL est **transformée en spread** (logique prudente, linéaire dans un premier temps).

---

### 4. 📊 Scénarios économiques

3 scénarios disponibles :
- **Normal** : notation inchangée
- **Stress** : dégradation d’un notch
- **Recovery** : amélioration d’un notch

Les spreads sont recalculés à chaque simulation.

---

### 5. 🧮 Valorisation

Fonction `present_value()` :
- Actualise chaque cash flow selon le taux ajusté
- Calcule la **valeur actuelle de l’obligation** dans chaque scénario

---

### 6. 📉 Visualisations

Graphiques générés dans le notebook :
- Prix vs notation (avec et sans ajustement)
- Impact du spread sur la VAN
- Stress test : effet d’une crise sectorielle sur le prix
- Comparaison entre scénarios (delta de prix)

---

## 📁 Structure technique du projet
