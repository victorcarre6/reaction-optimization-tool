# Extraction de données à partir de l'Open Reaction Database (ORD)

Ce script Python extrait automatiquement des informations chimiques clés à partir d’un fichier `.pb` de l’Open Reaction Database (ORD), afin de générer un fichier `.csv` structuré pour l’analyse ou le machine learning.

## Fichier généré

Le fichier `buchwald_full.csv` contient les colonnes suivantes :

| Colonne                        | Description |
|-------------------------------|-------------|
| `reaction_id`                 | ID global de la réaction |
| `reaction_index_CUSTOM`      | Identifiant interne spécifique (type 1) |
| `reaction_type`              | Type de réaction (type 5) |
| `inputs_*_SMILES`            | SMILES concaténés des différents inputs (réactifs, solvants, etc.) |
| `temperature_Celsius`        | Température de réaction en °C |
| `yield_percent`              | Rendement chimique (entre 0 et 100) |

## Fonctionnement du script

### 1. Lecture du fichier `dataset.pb`

Le fichier binaire est chargé via les objets `reaction_pb2`.

```python
from ord_schema.proto import reaction_pb2
```

### 2. Extraction des identifiants

Certains identifiants comme `reaction_index_CUSTOM` ou `reaction_type` sont extraits via leurs *codes numériques* respectifs :

```python
reaction_index_custom = get_identifier_value(reaction.identifiers, 1)
reaction_type = get_identifier_value(reaction.identifiers, 5)
```

### 3. SMILES des réactifs

Les inputs sont regroupés en catégories normalisées :

- `metal and ligand`
- `aryl halide`
- `amine`
- `solvent`
- `base`

La structure SMILES est extraite uniquement pour les identifiants de type `SMILES` (code `2`).

```python
if iden.type == 2:  # SMILES
    smiles_list.append(iden.value)
```

### 4. Température de réaction

La température est extraite si elle est définie :

```python
if reaction.conditions.temperature.setpoint:
    temp_c = reaction.conditions.temperature.setpoint.value
```

### 5. Rendement chimique

Le rendement est défini via un `measurement` de type `YIELD` (code `3`) associé au produit principal (`is_desired_product = True`).

```python
if meas.type == 3:
    yield_percent = round(100 * meas.percentage.value, 2)
```

## Exemple de ligne extraite

| reaction_id | reaction_index_CUSTOM | reaction_type | inputs_metal_and_ligand_SMILES | inputs_aryl_halide_SMILES | ... | temperature_Celsius | yield_percent |
|-------------|------------------------|---------------|-------------------------------|----------------------------|-----|----------------------|----------------|
| RXN-00123   | RXN-00123_CUSTOM       | Suzuki        | [Pd]                          | C1=CC=C(Br)C=C1            | ... | 100                  | 88.5           |

## Pistes d'amélioration

- Ajout d’une visualisation des distributions de rendement
- Intégration avec une base de données relationnelle ou NoSQL
- Utilisation pour entraîner un modèle de prédiction du rendement chimique

## Ressources

- https://docs.open-reaction-database.org/
- https://github.com/Open-Reaction-Database/ord-schema

## Auteur

Projet personnel de Victor Carré, docteur en photochimie, dans le cadre de son exploration en data science appliquée à la chimie.
