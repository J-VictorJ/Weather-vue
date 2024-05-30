<script setup>
import {ref} from 'vue';
import SearchInput from './components/SearchInput.vue';
import WeatherCard from './components/WeatherCard.vue';


const places = ref([]);
const addPlace = (data) => {
  places.value.push(data);
}

const deletePlace = (name) => {
  places.value = places.value.filter((p) => p.location.name !== name);
}
</script>
<template>
  <div id="app" class="min-h-screen bg-zinc-100 p-8 flex justify-center items-center">
    <main>
    <!--Date-->
    <div class="text-center mb-6">
      {{ new Date().toLocaleDateString('pt-br',{
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
      })
       }}
    </div>
    <!--Search-->
    <div>
      <SearchInput @place-data="addPlace"/>
    </div>
    
    <!-- Weather Cards -->
    <div class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-2 xl:grid-cols-3 gap-4">
        <div v-for="(place, idx) in places" :key="idx" class="max-w-xs md:max-w-sm lg:max-w-md xl:max-w-lg flex justify-center">
          <WeatherCard :place="place" @delete-place="deletePlace" class="mx-auto" />
        </div>
      </div>
    </main>
  </div>
  
</template>