<script setup>
import { ref } from 'vue';

const felelok = ref([])
let name = ref("")
let isHiba = ref(false)
let maiFelelo = ref("")


const addfelelo = () => {
   if (name.value == "") {
      isHiba.value = true
   }
   else {
      isHiba.value = false
      felelok.value.push(name.value)
   }
}

const deleteFelelo = (key) => {
   felelok.value.splice(key, 1)
}

function getRndInteger(min, max) {
   return Math.floor(Math.random() * (max - min)) + min;
}
const randomFelelo = () => {
   let random = getRndInteger(0, felelok.value.length)

   maiFelelo.value = felelok.value[random]
}

const reset = () => {
   felelok.value = []
   maiFelelo.value = ""
}

</script>

<template>
   <div id="names" class="container">
      <div class="logo">
         <h1>Felelő sorsoló</h1>
      </div>

      <div class="input_container">
         <input title="név" placeholder="Ide írj egy nevet!" type="text" v-model="name" />
         <button @click="addfelelo">Név felvétele</button>
      </div>

      <div class="error_label" v-if="isHiba">
         <p>A név mező nem lehet üres</p>
      </div>

      <div class="list_of_names">
         <ul>
            <!-- Ide lesznek kiírva a sorsolandó nevek a lista alapján -->
            <li v-for="(felelo, key) in felelok" @click="deleteFelelo(key)">{{ felelo }}</li>
         </ul>
      </div>

      <div v-if="felelok.length>=2">
         <!-- Ez a div csak akkor jelenjen meg, ha van legalább 2 név a listában -->
         <button @click="randomFelelo">Ki lesz a felelő?</button>
      </div>

   </div>

   <div id="result" class="container">
      <div class="result_container">
         <h1>A felelő: </h1>
         <div class="result_value">
            <!-- Ide lesz kiírva a kisorsolt felelő -->
            <h1>{{ maiFelelo }}</h1>
         </div>

         <button @click="reset">Újra kezdés</button>

         <button @click="randomFelelo">Nem tetszik, kérek egy másikat</button>
      </div>
   </div>
</template>

<style scoped></style>
