# Query 1 : `palmares 1`

**Description:**  
Retrieves performance values for a specific franchise (with ID = 1) across all statistics.

```sql
SELECT Statistiques.libelle, [Réaliser II].perf_franchise
FROM Statistiques 
INNER JOIN (
    Franchises 
    INNER JOIN [Réaliser II] 
    ON Franchises.id_franchise = [Réaliser II].id_franchise
) 
ON Statistiques.id_statistique = [Réaliser II].id_statistique
WHERE Franchises.id_franchise = 1;
```

# Query 2: `sponsor1`

**Description:**  
Retrieves the sponsor(s) associated with a specific franchise (with ID = 1)

```sql
SELECT Franchises.id_franchise, Franchises.nom_franchise, Sponsors.nom_sponsor
FROM Sponsors 
INNER JOIN (
    Franchises 
    INNER JOIN Sponsoring 
    ON Franchises.id_franchise = Sponsoring.id_franchise
) 
ON Sponsors.id_sponsor = Sponsoring.id_sponsor
WHERE Franchises.id_franchise = 1;
```