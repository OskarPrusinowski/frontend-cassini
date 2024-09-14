<template>
    <div>
        <!-- Navbar Section -->
        <header class="container">
            <nav class="navbar navbar-expand-lg navbar-dark">
                <a class="navbar-brand" href="#">
                    <img src="logo.png" alt="SAP Logo" style="width: 50px;">
                </a>
                <div class="collapse navbar-collapse">
                    <ul class="navbar-nav ml-auto">
                        <li class="nav-item"><a class="nav-link" href="#">Strona Główna</a></li>
                        <li class="nav-item"><a class="nav-link" href="#">O Nas</a></li>
                        <li class="nav-item"><a class="nav-link" href="#">Usługi</a></li>
                        <li class="nav-item"><a class="nav-link" href="#">Kontakt</a></li>
                    </ul>
                </div>
            </nav>
        </header>

        <!-- Main Section -->
        <section class="main-section container">
            <div>
                <h1>Let's give farmers even more climate take a look...</h1>
                <p>Tools and satellite data to improve the efficiency of your land!</p>
                <p class="scroll-down">Scroll down to find out on your own!</p>
            </div>
            <div>
                <img src="lol/img/1.jpg" class="rounded-circle" style="box-shadow: -10px 7px 10px 5px #0d076d;"
                    alt="...">
            </div>
        </section>

        <!-- Map Section -->
        <h1 style="margin-top: 30vh;">Wybierz lokalizację na mapie</h1>
        <div id="map"></div>
        <button @click="goToLocation">Idź do lokalizacji w Google Maps</button>

        <!-- Footer Section -->
        <footer class="container text-center mt-5">
            <p>© 2024 SAP. All rights reserved.</p>
            <div>
                <a href="#">Polityka prywatności</a> |
                <a href="#">Warunki korzystania</a> |
                <a href="#">Kontakt</a>
            </div>
            <div class="mt-3">
                <a href="#"><img src="facebook-icon.png" alt="Facebook" style="width: 30px;"></a>
                <a href="#"><img src="twitter-icon.png" alt="Twitter" style="width: 30px;"></a>
                <a href="#"><img src="linkedin-icon.png" alt="LinkedIn" style="width: 30px;"></a>
            </div>
        </footer>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    data() {
        return {
            selectedLocation: { lat: 52.2297, lng: 21.0122 }, // Default location (Warsaw)
            map: null,
            marker: null
        };
    },
    mounted() {
        this.initMap();
    },
    methods: {
        initMap() {
            // Initialize Google Map
            this.map = new google.maps.Map(document.getElementById('map'), {
                center: this.selectedLocation,
                zoom: 8
            });

            // Add marker at the initial location
            this.marker = new google.maps.Marker({
                position: this.selectedLocation,
                map: this.map
            });

            // Add click listener to update marker position and location
            this.map.addListener('click', (event) => {
                this.selectedLocation = {
                    lat: event.latLng.lat(),
                    lng: event.latLng.lng()
                };
                this.updateMarker();
            });
        },
        updateMarker() {
            // Update marker position to the new selected location
            this.marker.setPosition(this.selectedLocation);
        },
        goToLocation() {
            // Open Google Maps at the selected location
            const url = `https://www.google.com/maps?q=${this.selectedLocation.lat},${this.selectedLocation.lng}`;
            window.open(url, '_blank');
        }
    }
};
</script>

<style scoped>
/* Custom styling */
body {
    background-color: #141767;
    color: white;
}

.main-section {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 50px;
}

.main-section img {
    border-radius: 50%;
    max-width: 100%;
}

.scroll-down {
    margin-top: 20px;
    font-size: 1.2em;
}

#map {
    height: 500px;
    width: 100%;
}

button {
    margin-top: 10px;
}
</style>