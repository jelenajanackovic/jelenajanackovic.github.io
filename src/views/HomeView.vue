<template>
  <div class="home">
    <h3 class="naslov fw-bold">Početna strana </h3>
    <div v-if="flights">
      <nav>
        <ul class="pagination">
          <li class="page-item">
            <button class="page-link text-dark" style="background-color: #f1f6fa"  type="button" @click="(e) => loadFirst()">First</button>
          </li>
          <li class="page-item">
            <button class="page-link text-dark" style="background-color: #f1f6fa" type="button" @click="(e) => loadPrev()">Previous</button>
          </li>
          <li class="page-item">
            <a class="page-link text-dark" style="background-color: #f1f6fa" href="#">{{ flights.number + 1 }}</a>
          </li>
          <li class="page-item">
            <button class="page-link text-dark" style="background-color: #f1f6fa" type="button" @click="(e) => loadNext()">Next</button>
          </li>
          <li class="page-item">
            <button class="page-link text-dark" style="background-color: #f1f6fa" type="button" @click="(e) => loadLast()">Last</button>
          </li>


        </ul>
      </nav>
      <table class="table  table-striped">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">BROJ LETA</th>
            <th scope="col">DESTINACIJA</th>
            <th scope="col">MODEL AVIONA</th>
            <th scope="col">VREME</th>
            <th scope="col">AKCIJA</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="flight in flights.content">
            <th scope="row">{{ flight.id }}</th>
            <td>{{ flight.flightNumber }}</td>
            <td>{{ flight.destination }}</td>
            <td>{{ flight.plane }}</td>
            <td>{{ new Date(flight.scheduledAt).toLocaleString('sr-RS') }}</td>
            <td><button type="button" class="btn btn-outline-secondary text-dark"
                @click="(e) => showDetails(flight.id)">Detalji</button>
            </td>
          </tr>

        </tbody>
      </table>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import FlightService from '@/services/flight.service'

const flights = ref();

function loadData(page = 0) {
  console.log(page)
  FlightService.getAllFlights(page, 12)
    .then(rsp => {
      console.log(rsp)
      flights.value = rsp.data
    })
}
loadData()

function loadFirst() {
  console.log("Ucitaj prvu")
  if (flights.value.first) return
  loadData()
}

function loadPrev(){
  console.log("Ucitaj prethodnu")
  if (flights.value.first) return
  loadData(flights.value.number -1)
}

function loadNext() {
  console.log("Ucitaj sledecu")
  if(flights.value.last) return
  loadData(flights.value.number +1)
}

function loadLast(){
  console.log("Ucitaj poslednju")
  if(flights.value.last) return
  loadData(flights.value.totalPages-1)
}




const router = useRouter()
function showDetails(id) {
  router.push('/flight/' + id)
}





</script>
<style>
h3.naslov{
color: black;
padding-left: 0px;
font-weight: 450;

}

body{
  height: 1000px;
  background-color: #f1f6fa;
}
</style>