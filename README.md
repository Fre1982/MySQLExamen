# MySQLExamen

Geef de namen van de Franstalige personen van wie de naam begint met een 'M'.
SELECT persoon_naam 
FROM persoon
WHERE persoontaal = 'F'
AND persoon_naam LIKE 'M';

Geef de referenties en de namen van de personen, gesorteerd volgens het referentienummer van hoog naar laag. Gebruik bij het sorteren een nummer in plaats van een kolomnaam.
SELECT persoon_id, persoon_naam
FROM persoon
ORDER BY 1 DESC; 

Geef de productcode en het productnummer van de producten waarbij een locatie is ingevuld.
SELECT product_code, product_nr
FROM product
WHERE locatie_nr IS NOT NULL;

Geef de productcode en het productnummer van de producten met een productnummer tussen de 5 en 15 en de producten met een productnummer tussen de 30 en 50.
SELECT product_code, product_nr
FROM product
WHERE product_nr BETWEEN 5 AND 15
OR product_nr BETWEEN 30 AND 50;

Geef de productcode en het productnummer van de producten met productnummer 5,10,20,25. Maak gebruik van IN.
SELECT product_code, product_nr
FROM product
WHERE product_nr IN(5, 10, 15, 20, 25);

Geef de naam en voornaam van de personen waarbij de laatste letter van de achternaam een 's' is en de eerste letter van de voornaam een 'f' of een 'p'.
SELECT persoon_naam, persoon_voornaam
FROM persoon
WHERE RIGHT(UPPER(persoon_naam),1) = 'S'
AND LEFT(UPPER(persoon_voornaam),1) IN ('F','P');

Geef de namen van de personen van de Nederlandstalige en/of Franstalige taalgroep, hun geslacht ('man' of 'vrouw') en hun taal ('Nederlandstalig' of 'Franstalig').
SELECT persoon_naam Naam, 'man' Geslacht, 'Nederlandstalig' Taal
FROM persoon
WHERE persoon_geslacht = 1
AND persoon_taal = 'N'
UNION
SELECT persoon_naam Naam, 'vrouw' Geslacht, 'Nederlandstalig' Taal
FROM persoon
WHERE persoon_geslacht = 2
AND persoon_taal ='N'
UNION
SELECT persoon_naam Naam, 'man' Geslacht, 'Franstalig' Taal
FROM persoon
WHERE persoon_geslacht = 1
AND persoon_taal = 'F'
UNION
SELECT persoon_naam Naam, 'vrouw' Geslacht, 'Franstalig' Taal
FROM persoon
WHERE persoon_geslacht = 2
AND persoon_taal ='F';

Hoeveel Franstalige personen zijn er?
SELECT COUNT(*) Aantal_Franstalige_Personen
FROM persoon
WHERE persoon_taal = 'F'; 

Geef de productcode en het productnummer van de producten waarbij geen oorsprong is ingevuld.
SELECT product_code, product_nr
FROM product
WHERE oorsprong_nr IS NULL;

Geef de productcode, het productnummer en de naam van de locatie. In de gevallen dat de naam van de locatie niet is ingevuld, moet er in die plaats geen worden vermeld.
SELECT pr.product_code, pr.product_nr, NVL(lo.locatie_naam, 'geen')
FROM product pr LEFT OUTER JOIN locatie lo
ON (pr.locatie_nr = lo.locatie_id);


geef de namen van de locaties waarvan de naam uit 16 letters bestaat, maar waarin het woord 'Magazijn' voorkomt.
SELECT locatie_naam
FROM locatie
WHERE LEN(locatie_naam) = 16
AND locatie_naam LIKE '%Magazijn%';

Geef de productcode en het productnummer van de producten met productcode 'HA' of 'NE' maar waarvan het productnummer kleiner is dan 15.
SELECT product_code,product_nr 
FROM product 
WHERE (product_code='HA' OR product_code='NE') 
AND product_nr<15;

Geef de productcode en het nummer van die producten waarbij de naam van de locatie begint met 'maga'. Maak gebruik van de principes van Subquery.
SELECT pr.product_code, pr.product_nr
FROM product pr
WHERE EXIST 	(SELECT lo.locatie_naam
		FROM locatie lo
		WHERE lo.locatie_id = pr.locatie_nr
		AND LOWER(lo.locatie_naam) LIKE 'maga%');

Verhuis alle producten van magazijn 1 naar magazijn 2.
UPDATE product
SET locatie_nr = 2
WHERE locatie_nr = 1;

Verwijder alle producten van Millie.
DELETE FROM product 
WHERE oorsprong _nr = 14;
