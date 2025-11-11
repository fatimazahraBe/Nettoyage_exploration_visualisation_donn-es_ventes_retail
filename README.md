<h1>Identification des Hypothèses et Analyse des Données</h1>



 <strong>1. Analyse de l'intégrité des données</strong><br>
<strong> Transaction ID :</strong><br>
 Nous avons identifié 12 575 identifiants de transaction distincts, ce qui confirme l'absence de doublons dans notre jeu de données. Chaque transaction est unique.<br>
<strong>Customer ID et Catégories de produits :</strong><br>
L'analyse révèle 25 identifiants clients uniques et 8 catégories de produits. Théoriquement, la combinaison de ces deux dimensions devrait produire 200 items distincts (25 × 8 = 200). Cependant, nous observons 201 items distincts.<br>
<strong>Item (Nom du produit) :</strong><br>
Cette différence s'explique par la présence de valeurs manquantes représentant 10% des données dans la colonne "Item". 
Étant donné que l'identification précise du nom du produit n'est pas essentielle
pour notre analyse (nous disposons déjà de la catégorie), nous décidons de remplacer ces valeurs 
null par la mention "Non spécifié".<br>
<strong>2. Traitement des valeurs manquantes dans les colonnes financières</strong><br>
<strong>Observation :</strong><br>
Les colonnes Price, Quantity et Total Spent présentent chacune <strong> 5% </strong>de valeurs manquantes. 
Relation mathématique identifiée :
<srtong>Total Spent = Price × Quantity</srtong><br>
<strong>Stratégie de remplissage logique :</strong><br>

<strong>Cas 1 :</strong> Total manquant : Si Price et Quantity sont disponibles<br>
<strong>Total Spent = Price × Quantity</strong><br>
<strong>Cas 2 :</strong>  Price manquant : Si Total Spent et Quantity sont disponibles<br>
<strong>Price = Total Spent ÷ Quantity</strong><br>
<strong>Cas 3 :</strong> Quantity manquante : Si Total Spent et Price sont disponibles<br>
<strong>Quantity = Total Spent ÷ Price</strong><br>
<strong>Cas 4 :</strong>  Deux variables ou plus manquantes : Impossible de reconstituer l'information de manière fiable<br>
Suppression de la ligne concernée<br>
<strong>3. Analyse des variables catégorielles</strong><br>
<strong>Payment Method (Méthode de paiement) :</strong><br>
<strong>Trois modalités identifiées : </strong>Cash (Espèces), Card (Carte bancaire), et Digital Wallet (Portefeuille numérique). Aucune valeur manquante détectée.<br>
<strong>Location (Point de vente) :</strong><br>
<strong>Deux modalités distinctes :</strong> Online (En ligne) et In-Store (En magasin). Les données sont complètes.<br>
<strong>Transaction Date :</strong><br>
Format de date cohérent et uniforme. Aucune anomalie détectée.<br>
<strong>Discount (Réduction appliquée) :</strong><br>
<strong>Trois valeurs distinctes observées :</strong> True (Oui), False (Non), et null (Non renseigné). Les valeurs null représentent les transactions pour lesquelles l'information sur la réduction n'a pas été enregistrée. Nous décidons de remplacer ces valeurs null par "Unknone" .
