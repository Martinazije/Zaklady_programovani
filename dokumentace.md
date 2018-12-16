# Dokumentace - úkol č. 2
Program na základě metody quadtree rozděluje data na shluky bodů o počtu maximálně 50. Každý bod dostane ID shluku, ve kterém se nachází. Pokud shluk obsahuje více než 50 bodů, dochází k dalšímu dělení na 4 sektory a další přiřazování ID.
## Vstupní program
Vstupním programem je GeoJSON soubor s bodovou vrstvou.
## Výstupní program
Výstupním programem je GeoJSON soubor s bodovou vrstvou a ID.
## Průběh
Po načtení souboru GeoJSON se provede kontrola toho, zda vstupní parametry splňují podmínky pro spuštění programu. Data se načtou do seznamu.
### Get_x_half, Get_y_half
Dochází ke zjištění středových souřadnic, na základě kterých se pak budou data dělit do 4 sektorů. 
### Rozrazeni
Na začátku samotné rekurze se kontroluje, zda už vstup neobsahuje méně než 50 bodů. Pokud ne, dochází k vytvoření seznamů k 4 sektorům, do kterého jsou na základě středových souřadnic shluku bodů rozřazovány do 4 sektorů. Poté se zjišťuje, kolik bodů každý sektor obsahuje. Pokud je to nad 50 bodů, volá se znova funkce rozdělení. 
###
Výstupní soubor obsahuje všechny body a ID sektoru, ve kterém se nachází.

