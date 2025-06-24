#  Main Tables

## 1. `Franchises`

Represents the teams in the league.

| Field             | Type        | Description                     |
|------------------|-------------|---------------------------------|
| id_franchise      | Integer     | Unique identifier for the franchise |
| nom_franchise     | Text        | Team name                       |
| année_creation    | Integer     | Year of creation                |
| ville             | Text        | City of origin                  |
| stade             | Text        | Home stadium                    |
| conference        | Text        | Conference (East / West)        |
| logo              | Text        | Logo reference (optional)       |



## 2. `Personnes` (People)
Contains information about members (players, coaches, etc.).

| Field          | Type    | Description                            |
|----------------|---------|----------------------------------------|
| id_personne    | Integer | Person ID                              |
| nom, prenom    | Text    | Last name and first name               |
| age            | Integer | Age of the person                      |
| id_fonction    | Integer | Role/function reference                |
| id_franchise   | Integer | Franchise reference                    |
| dossard        | Integer | Jersey number (optional)               |
| photo          | Text    | Photo link or object                   |


## 3. `Fonctions` (Functions/Roles)
Lists the roles (coach, player, etc.).

| Field            | Type    | Description         |
|------------------|---------|---------------------|
| id_fonction      | Integer | Primary key         |
| libelle_fonction | Text    | Role name           |



## 4. `Matchs`
Represents games between two franchises.

| Field             | Type    | Description                      |
|------------------|---------|----------------------------------|
| id_match         | Text    | Match ID                         |
| id_franchise_1   | Integer | First franchise                  |
| id_franchise_2   | Integer | Second franchise                 |
| date_match       | Date    | Date of the match                |
| heure_match      | Time    | Time of the match                |
| ville_match      | Text    | City where the match is held     |
| point_franch_1   | Integer | Score of the first team          |
| point_franch_2   | Integer | Score of the second team         |
| phase            | Text    | Competition phase                |



## 5. `Participer` (Participation)
Join table linking people and matches.

| Field        | Type    | Description                           |
|-------------|---------|---------------------------------------|
| id_personne | Integer | Person ID                             |
| id_match    | Text    | Match ID                              |



## 6. `Statistiques` (Statistics)
Lists the types of statistics tracked (points, rebounds, etc.).

| Field          | Type    | Description              |
|----------------|---------|--------------------------|
| id_statistique | Text    | Statistic ID             |
| libelle        | Text    | Statistic label          |


## 7. `Réaliser I` (Individual Stats)
Links a person to a given statistic.

| Field          | Type    | Description                            |
|----------------|---------|----------------------------------------|
| id_personne    | Integer | Person reference                       |
| id_statistique | Text    | Statistic reference                    |
| performance    | Integer | Measured value                         |


## 8. `Réaliser II` (Team Stats)
Aggregated statistics by franchise.

| Field           | Type    | Description                            |
|-----------------|---------|----------------------------------------|
| id_franchise    | Integer | Franchise reference                    |
| id_statistique  | Text    | Statistic reference                    |
| perf_franchise  | Double  | Measured value                         |

---

## 9. `Sponsors`
List of league sponsors.

| Field              | Type    | Description                     |
|--------------------|---------|---------------------------------|
| id_sponsor         | Integer | Sponsor ID                      |
| nom_sponsor        | Text    | Sponsor name                    |
| année_creation_sp  | Integer | Year founded                    |
| siege_social       | Text    | Headquarters                    |
| secteur_activité   | Text    | Business sector                 |
| Photo              | Text    | Logo or image                   |


## 10. `Sponsoring`
Join table between sponsors and franchises.

| Field          | Type    | Description                              |
|----------------|---------|------------------------------------------|
| id_franchise   | Integer | Sponsored franchise reference            |
| id_sponsor     | Integer | Sponsor reference                        |
| type_apport    | Text    | Nature of support (financial, logistical...) |



# Relationships

| # | Table 1         | Table 2         | Foreign Key Field           | Type        |
|--:|------------------|------------------|-----------------------------|-------------|
| 1 | `Personnes`      | `Fonctions`      | `id_fonction`               | 1 → N       |
| 2 | `Personnes`      | `Franchises`     | `id_franchise`              | 1 → N       |
| 3 | `Personnes`      | `Participer`     | `id_personne`               | 1 → N       |
| 4 | `Personnes`      | `Réaliser I`     | `id_personne`               | 1 → N       |
| 5 | `Matchs`         | `Franchises`     | `id_franchise`              | 1 → N       |
| 6 | `Matchs`         | `Participer`     | `id_match`                  | 1 → N       |
| 7 | `Statistiques`   | `Réaliser I`     | `id_statistique`            | 1 → N       |
| 8 | `Statistiques`   | `Réaliser II`    | `id_statistique`            | 1 → N       |
| 9 | `Réaliser II`    | `Franchises`     | `id_franchise`              | 1 → N       |
|10 | `Sponsoring`     | `Franchises`     | `id_franchise`              | 1 → N       |
|11 | `Sponsoring`     | `Sponsors`       | `id_sponsor`                | 1 → N       |
