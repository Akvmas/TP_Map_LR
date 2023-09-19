document.addEventListener("DOMContentLoaded", async function () {
    // Sélectionnez l'élément tbody du tableau
    var tableBody = document.getElementById('lieux-liste');

    try {
        // Charger les données depuis le fichier JSON
        const response = await fetch('data.json');
        const data = await response.json();

        // Utiliser forEach pour parcourir toutes les données
        data.forEach(function (lieu) {
            var row = document.createElement('tr');
            var adresseCell = document.createElement('td');
            adresseCell.textContent = lieu.fields.adresse;
            var latitudeCell = document.createElement('td');
            latitudeCell.textContent = lieu.geometry.coordinates[1];
            var longitudeCell = document.createElement('td');
            longitudeCell.textContent = lieu.geometry.coordinates[0];
            row.appendChild(adresseCell);
            row.appendChild(latitudeCell);
            row.appendChild(longitudeCell);
            tableBody.appendChild(row);
        });
    } catch (error) {
        console.error('Erreur de chargement des données :', error);
    }
});


<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="script.js"></script>
    <title>Visionnage des lieux</title>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>Adresse</th>
                <th>Latitude</th>
                <th>Longitude</th>
            </tr>
        </thead>
        <tbody id="lieux-liste">
        </tbody>
    </table>
</body>
</html>