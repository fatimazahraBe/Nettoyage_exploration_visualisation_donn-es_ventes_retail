# Retail Store Sales Analysis - Documentation

## 📅 Documentation - Day 1 (10/11/2025)

### Step 1: Data Loading

- **File Name:** `retail store sales.csv`
- **Import Method:** Loaded into Power BI using Power Query.
- **Settings:** Encoding `UTF-8`, Delimiter `Comma`.

### 🏗️ Initial Structure
- **Rows:** 12,575
- **Columns:** 11

### 🧐 Initial Data Quality Observations

| Column Name | Data Type | Validity | Notes / Missing Values |
| :--- | :--- | :--- | :--- |
| **Transaction ID** | Text | 100% | All values valid and unique. |
| **Customer ID** | Text | 100% | All values valid. |
| **Category** | Text | 100% | All values valid (8 distinct values). |
| **Item** | Text | 90% | **1,213** empty rows. |
| **Price Per Unit** | Number | 95% | **609** empty rows. |
| **Quantity** | Int | 95% | **604** empty rows. |
| **Total Spent** | Number | 95% | **604** empty rows. |
| **Payment Method**| Text | 100% | All values valid. |
| **Location** | Text | 100% | All values valid. |
| **Transaction Date**| Date | 100% | All values valid. |
| **Discount Applied**| Logical | 67% | **4,199** empty rows. |

---

## 🚀 Documentation - Jour 2 : Identification des Hypothèses et Analyse des Données

### 1. Analyse de l'intégrité des données

![etat_init](https://github.com/user-attachments/assets/e9af2762-eb52-4077-a4ac-5603e7fb4b29)

- **Transaction ID :**
  - Nous avons identifié **12 575** identifiants de transaction distincts.
  - ✅ **Conclusion :** Absence de doublons, chaque transaction est unique.

- **Customer ID et Catégories de produits :**
  - L'analyse révèle **25** identifiants clients uniques et **8** catégories de produits.
  - *Théorie :* La combinaison de ces deux dimensions devrait produire 200 items (25 × 8).
  - *Observation :* Nous observons **201** items distincts.

- **Item (Nom du produit) :**
  - L'écart ci-dessus s'explique par la présence de valeurs manquantes (**10%** des données) dans la colonne `Item`.
  - 🛠 **Décision :** L'identification précise du nom du produit n'étant pas essentielle (la catégorie suffit), nous remplaçons les valeurs `null` par **"Non spécifié"**.

### 2. Traitement des valeurs manquantes dans les colonnes financières

![etat_init2](https://github.com/user-attachments/assets/602c3e92-bb5f-46ef-b5c1-bff9cc807f71)

**Observation :**
Les colonnes `Price`, `Quantity` et `Total Spent` présentent chacune **5%** de valeurs manquantes.

**Relation Mathématique :**
> **Total Spent = Price × Quantity**

**Stratégie de remplissage logique :**

| Cas de figure | Variables Disponibles | Formule Appliquée |
| :--- | :--- | :--- |
| **Cas 1 : Total manquant** | Price, Quantity | `Total Spent = Price × Quantity` |
| **Cas 2 : Price manquant** | Total Spent, Quantity | `Price = Total Spent ÷ Quantity` |
| **Cas 3 : Quantity manquante** | Total Spent, Price | `Quantity = Total Spent ÷ Price` |
| **Cas 4 : 2+ variables manquantes** | Insuffisantes | 🗑 **Suppression de la ligne** (Impossibilité de reconstituer l'info de manière fiable). |

### 3. Analyse des variables catégorielles

- **Payment Method (Méthode de paiement) :**
  - **3 modalités :** Cash (Espèces), Card (Carte bancaire), Digital Wallet (Portefeuille numérique).
  - ✅ Aucune valeur manquante.

- **Location (Point de vente) :**
  - **2 modalités :** Online (En ligne), In-Store (En magasin).
  - ✅ Données complètes.

- **Transaction Date :**
  - ✅ Format de date cohérent et uniforme. Aucune anomalie.

- **Discount (Réduction appliquée) :**
  - **3 valeurs :** `True` (Oui), `False` (Non), et `null`.
  - *Analyse :* Les valeurs `null` indiquent que l'info n'a pas été enregistrée.
  - 🛠 **Décision :** Remplacement des `null` par **"Unknown"**.
