<template>
    <div class='flight p-3 mb-2 bg-secondary  text-white'>
        <div v-if="flight && mapData && weather">
            <h3 class="text-center">Detalji leta</h3>
            <div class="card w-75 mx-auto mt-3">
                <img :src="'https://img.pequla.com/destination/' + flight.destination.toLowerCase().split(' ')[0] + '.jpg'"
                    class="card-img-top">
                <div class="naslov">
                    <h5 class="card-title ">{{ mapData.items[0].title }}</h5>

                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Broj leta: {{ flight.flightNumber }}</li>
                    <li class="list-group-item">Trenutna temperatura: {{ toCelsious(weather.current.temp) }}</li>
                    <li class="list-group-item">Osecaj: {{ toCelsious(weather.current.feels_like) }}</li>
                    <li class="list-group-item">Vlaznost vazduha: {{ weather.current.humidity }}%</li>
                </ul>
                <div>
                    <iframe class="mx-auto" width="100%" height="500"
                        :src="`https://www.google.com/maps?output=embed&q=${mapData.items[0].title}`" allowfullscreen=""
                        loading="lazy" referrerpolicy="no-referrer-when-downgrade" id="gmaps"></iframe>


                </div>

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
    padding-left: 15px;
    font-weight: 900;

}
</style>
