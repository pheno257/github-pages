<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF8"
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>HeathCare Appointment System</title>
        <link rel="stylesheet" href="style.css">
        </head>
        <body>
            <div class="background-image"></div>
            <div class="container">
                <header>
                    <h1>HealthCare Appointment system</h1>
                    <p>Book your appointment with the best doctors in your area.</p>
                    <p>
                        Welcome to HeathConnect, your one-stop-shop for all your healthcare needs.
                        our website is designed to provide comprehensive and accessible healthcare services to people of all ages and background.
                        With a team of experienced healthcare professionals, we offer personalized advice and guidance to help you make informed decisions about your health.
                        Our website features a vast library of health related articles, videos and resources, covering topics from nutrition and wellness to disease management and prevention.
                        We also offer Online Appointment Scheduling, prescription refill requests and secure messaging with our healthcare team.
                        Our goal is to empower you with the knowledge and tools you need to take control of your health and wellbeing.
                        We believe healthcare should be accessible, affordable, and compassionate, and we strive to reflect these values in everything we do.
                        Whether you're seeking medical advice, looking for health and wellness tips, or simply wanting to learn more about a particular health topic, we're here to help.
                        At HeathConnect, we're committed to providing high-quality, patient-centered care that meets the unique needs and preferences of each individual.
                         </p>
                </header>
                <main>
                    <form id="searchForm">
                        <input type="text" id="location" placeholder="Enter your location" required>
                        <button type="submit">Find Doctors</button>
                    </form>
                   
                    <div id="map"></div>
                </main>
                </div>
                <script src="script.js"></script>
                <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_GOOGLE_MAPS_API_KEY&callback=intMap" async defer></script>
                </body>
                </html>

                <style>

                body, html {
                    margin: 0;
                    background-color:#ffff00;
                    padding: 0;
                    front-family: Ariel, sans-serif;
                }

                .background-image {
                    position: fixed;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background-image:url('assets/heathCare-bg.jpg');
                    background-size: cover;
                    background-position: center;
                    z-index: -1;
                }

                .container {
                    position: relative;
                    z-index: 1;
                    text-align: center;
                    padding: 50px;
                    color: rgb(33, 194, 9);
                }
            
header h1 {
    front-size: 3rem;
    margin-bottom: 10px;
}

header p {
    front-size: 1.2rem;
}

#searchForm {
    margin-top: 20px;
}

#searchForm input {
    padding: 10px;
    width: 300px;
    border: none;
    border-radius: 5px;
}

#searchForm button {
    padding: 10px 20px;
    background-color: #007BFF;
    color: red;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

#map {
    margin-top: 20px;
    height: 400px;
    width: 100px;
    background-color: #7415c8;
}
</style>

<script>
let map

function initMap() {
    map = new google.maps.Maps(document.getElementById('map'), {
        center: { lat: -1.3733, lng: -32.2903 },
        zoom: 8,
    });
    


    fetch('backend/fetch_doctors.php')
    .then(response => response.json())
    .then(data => {
        data.forEach(doctor => {
            new google.maps.Market({
                position: { lat: parseFloat(doctor.lat), lng: parseFloat(doctor.lng) },
                map: map,
                title: doctor.name,
            });
        });
    });
}

document.getElementById('searchForm').addEventListener('submit', function (e) {
    e.preventDefault();
    const location = document.getElementById('location').value;
    alert('searching for doctors near ${location}...');
    // add logic to filter doctors by location
});
</script>

<script>
<?php
$servername = "localhost";
$username = "root";
$password = "";
$db name = "healthcare";

$conn = new MyQL($servername, $username, $password, $db name);

if ($conn->connect_error) {
    die("connection failed: " .$conn->connect_error);
}
?>
</style>

<style>
<?php
include 'db.php';

$sql = "SELECT name, lat, lng FROMdoctors";
$result = $conn->query($sql);

$doctors = [];
if ($result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
        $doctors[] = $row;
    }
}

echo json_encode($doctors);
$conn->close();
?>
</style>

<style>
CREATE TABLE doctors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    lat DECIMAL(30) NOT NULL,
    lng DECIMAL(20) NOT NULL
);

INSERT INTO doctors (name, lat, lng) VALUES
('Dr. Kamagezi Mary', 1.1006, -2.8930),
('Dr. Mugarura Dickens', 2.0067, -32.2903),
('Dr. Muhwezi Collins', 2.6780, -32.8900);
</style>
