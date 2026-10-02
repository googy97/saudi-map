<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>خريطة السعودية 🇸🇦</title>

    <link
        rel="stylesheet"
        href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
    >

    <style>
        * {
            box-sizing: border-box;
        }

        html,
        body {
            margin: 0;
            width: 100%;
            height: 100%;
        }

        body {
            background: #0f5132;
            font-family: Arial, sans-serif;
        }

        #map {
            width: 100%;
            height: 100vh;
            background: #0f5132;
        }

        .title {
            position: absolute;
            top: 20px;
            right: 20px;
            z-index: 1000;

            background: white;
            color: #174a3b;

            padding: 12px 20px;
            border-radius: 15px;

            font-size: 21px;
            font-weight: bold;

            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
    </style>
</head>

<body>

    <div class="title">
        🇸🇦 خريطة السعودية
    </div>

    <div id="map"></div>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>

        const map = L.map("map", {
            zoomControl: true,
            attributionControl: false
        });

        // ملف حدود السعودية فقط
        const saudiURL =
            "https://raw.githubusercontent.com/glynnbird/countriesgeojson/master/saudi%20arabia.geojson";

        fetch(saudiURL)
            .then(response => response.json())
            .then(data => {

                const saudi = L.geoJSON(data, {

                    style: {
                        fillColor: "#ffffff",
                        fillOpacity: 1,
                        color: "#174a3b",
                        weight: 3
                    }

                }).addTo(map);

                // تكبير الخريطة على السعودية
                map.fitBounds(saudi.getBounds(), {
                    padding: [30, 30]
                });

            })
            .catch(error => {

                console.error("حدث خطأ:", error);

                document.getElementById("map").innerHTML =
                    "<div style='color:white;text-align:center;padding:50px;font-size:20px'>حدث خطأ في تحميل خريطة السعودية</div>";

            });

    </script>

</body>

</html>
