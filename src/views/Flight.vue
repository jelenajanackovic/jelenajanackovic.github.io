<template>
    <div class='flight p-3 mb-2 text-white' style="background-color: #C7DBD2">
        <div v-if="flight && mapData && weather">
            <h3 class="text-center fw-bold" style="color: #666D72">Detalji leta</h3>


            <div class="card">
                <img :src="'https://img.pequla.com/destination/' + flight.destination.toLowerCase().split(' ')[0] + '.jpg'"
                    class="img">
                <div class="container-text">
                    <div class="naslov">
                        <h5 class="card-title ">{{ mapData.items[0].title }}</h5>

                    </div>
                    <ul class="list-group list-group-flush">
                        <li class="list-group-item" style="background-color: #C7DBD2">Broj leta: {{ flight.flightNumber }}</li>
                        <li class="list-group-item" style="background-color: #C7DBD2">Trenutna temperatura: {{ toCelsious(weather.current.temp) }}</li>
                        <li class="list-group-item" style="background-color: #C7DBD2">Osecaj: {{ toCelsious(weather.current.feels_like) }}</li>
                        <li class="list-group-item" style="background-color: #C7DBD2">Vlaznost vazduha: {{ weather.current.humidity }}%</li>
                    </ul>
                </div>
            </div>
            <div class="mapa-container">
                <iframe class="mapa"
                    :src="`https://www.google.com/maps?output=embed&q=${mapData.items[0].title}`" allowfullscreen=""
                    loading="lazy" referrerpolicy="no-referrer-when-downgrade" id="gmaps"></iframe>


            </div>


        </div>
    </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
import { ref } from 'vue';
import WeatherService from '@/services/weather.service'
import FlightService from '@/services/flight.service'
const route = useRoute();
const id = route.params.id

const flight = ref();
const mapData = ref();
const weather = ref();

FlightService.getFlightById(id)
    .then(rsp => {
        flight.value = rsp.data

        WeatherService.geocode(rsp.data.destination)
            .then(rsp => {
                mapData.value = rsp.data


                const pos = rsp.data.items[0].position
                WeatherService.getWeatherData(pos)
                    .then(rsp => {
                        weather.value = rsp.data


                    })

            })

    })

function toCelsious(p) {
    return Math.round(p - 273.15)
}

</script>
<style>
.naslov {
    color: gray;
    font-weight: 900;
    

}

.card {
    margin: 0 auto;
    padding: 10px;
    display: flex;
    flex-direction: row;
    background-color: #E3F2FD;


}
.card img{
    width: 750px; 
    border-radius: 5px;
    border:10px solid #C7DBD2;

}
.container-text{
    
    margin: auto auto;
    padding: 20px;
    
}

.naslov h5{
    padding:0;
    text-align: center;
}

.mapa-container {
    width: 75%;
    height: 300px;
    margin: 0 auto;
    text-align: center;
    margin-top: 18px;

    
    
  
    
}
.mapa{
    width: 750px;
    height: 300px;
    border:10px solid #E3F2FD;
    border-radius: 5px;
}
</style>
