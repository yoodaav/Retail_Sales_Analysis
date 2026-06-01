# 🔍 Retail Sales Analytics – DuckDB + SQL dans Jupyter

## Ce que j’ai fait 
--- 
J’ai utilisé **DuckDB** comme SGBD directement sur le Notebook Python avec JupySQL.
---

---

## 📋 Les requêtes que j’ai exécutées

| # | Objectif | Fonction SQL |
|---|----------|---------------|
| 1 | Charger le CSV dans une table | `CREATE TABLE ... read_csv_auto()` |
| 2 | Voir les années dispo | `YEAR(Order_Date) GROUP BY` |
| 3 | Revenu total par année | `SUM(Revenue) GROUP BY YEAR` |
| 4 | Revenu par année + produit | `GROUP BY YEAR, Product` |
| 5 | Classer les produits par année | `DENSE_RANK() OVER(PARTITION BY YEAR ORDER BY SUM(Revenue) DESC)` |
| 6 | **Top 3 ventes par année** | CTE + `WHERE Rang BETWEEN 1 AND 3` |
| 7 | Classer les produits par catégorie | `DENSE_RANK() OVER(PARTITION BY Category)` |
| 8 | **Top 3 ventes par catégorie** | CTE + `WHERE Classement BETWEEN 1 AND 3` |
| 9 | Classer les produits par région (revenu) | `DENSE_RANK() OVER(PARTITION BY Region)` |
| 10 | **Top 5 ventes par région (revenu)** | CTE + `WHERE Classement BETWEEN 1 AND 5` |
| 11 | Compter les commandes par région + produit | `COUNT(DISTINCT Order_ID)` |
| 12 | **Top 5 ventes par région (volume)** | CTE + classement sur le nombre de commandes |
| 13 | Compter les commandes par catégorie + produit | `COUNT(DISTINCT Order_ID) GROUP BY Category, Product` |
| 14 | **Top 5 ventes par catégorie (volume)** | CTE + classement |

---

## 🧠 Ce que ces requêtes m’ont appris

- **Les 3 meilleurs produits de 2019** : Adidas Shoes, Boat Earbuds, Dell Laptop  
- **Les 3 meilleurs produits de 2020** : iPhone 14, Sony Headphones, iPad  
- **Par catégorie (revenu)** : Canon Camera (Electronics), Adidas Shoes (Fashion), Sony Headphones (Accessories)  
- **Par région (volume)** : Puma T-shirt domine dans l’Ouest, Sony Headphones dans le Nord, iPhone 14 à l’Est  


---
## 📊 Ce que j’ai mesuré

| Métrique | Requête SQL utilisée |
|----------|----------------------|
| Chiffre d’affaires (`Revenue`) | `SUM(Revenue)` |
| Volume de commandes | `COUNT(DISTINCT Order_ID)` |
| Classement | `DENSE_RANK() OVER(PARTITION BY ...)` |

---

## 🔥 Résultats clés (à retenir)

### 🏆 Par année (chiffre d’affaires)

| Année | Top produit | Revenu |
|-------|-------------|--------|
| 2019  | Adidas Shoes | **31,2 M€** |
| 2020  | iPhone 14    | **31,5 M€** |

### 👟 Par catégorie (revenu)

- **Electronics** → Canon Camera (58,1 M€)  
- **Fashion** → Adidas Shoes (56,6 M€)  
- **Accessories** → Sony Headphones (56,8 M€)  

### 🌍 Par région (volume de ventes)

- **North** → Sony Headphones (119 commandes)  
- **East** → iPhone 14 (118 commandes)  
- **West** → Puma T-shirt (121 commandes)  

---

## 🧠 Pourquoi ce projet est utile ?

- Identifier les **produits locomotives**  
- Optimiser les **stocks par région**  
- Prendre des décisions  rapidement  

---

## ⚙️ Technos utilisées

- `DuckDB` – base de données embarquée ultra-rapide  
- `JupySQL` – SQL interactif dans Jupyter  
- `Pandas` – affichage et manipulation légère  

---
## 🛠️ Stack technique

```python
import duckdb
%load_ext sql
%sql duckdb:///
