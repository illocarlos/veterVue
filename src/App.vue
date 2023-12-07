<script setup>
import Header from './components/Header.vue' 
import Form from './components/Form.vue'
import EachPacient from './components/Paciente.vue';
import { ref, reactive, watch, onMounted } from 'vue';
import{uid}from"uid"


const pacients = ref([])

// aunque este objeto es la creacion  la tiene en el form la buena practica es poder tenrlo lo mas arriba posible
// para poder pasarlo como prop en este caso al componente form o al componente pacienbte

const formPacient = reactive({
  id:null,
  pet: "",
  propietary: "",
  email: "",
  symptoms: "",
  high: "",

})



// tanto el watch como el onmounted declara es exactamente igual que el proyecto de las guittarras 
// simplemente es para guardar los datos  en el localStorage
watch(pacients, () => {
  addLocalStorage();
}, { deep: true });

onMounted(() => {
  pacients.value=[]

  const pacientStorage = localStorage.getItem('pacients')
  pacientStorage ? pacients.value = JSON.parse(pacientStorage) : console.log('vacio')
})

const addLocalStorage = () => {
  localStorage.setItem('pacients', JSON.stringify(pacients.value))
}


const savePacient = () => {

  if (formPacient.id) {
const {id}= formPacient
const i = pacients.value.findIndex((eachPasient)=> eachPasient.id===id)
    pacients.value[i]={...formPacient }
  } else {
    pacients.value.push({
      ...formPacient,
      id: uid(6)
    })

  }
// esto es una forma de resetear el formulario o valores del objeto
    // pet: "",
    // propietary: "",
    // email: "",
    // symptoms: "",     
    // high: "",
          
//esta la veo mas legible y es lo mismo 
  Object.assign(formPacient, {
    id:null,
    pet: "",
    propietary: "",
    email: "",
    symptoms: "",
    high: "",
    //con el espreit operator que hace una copia de ese objeto y el objet.assing de formPacient que 
    // vuelve al estado vacio el objeto al ser reactivo 
  })
}
const update = (id) => {
  const pacientUpdate = pacients.value.filter(pacient => pacient.id === id)[0]

  Object.assign(formPacient, pacientUpdate)
}

const deleted = (id) => {
    pacients.value = pacients.value.filter(elem => elem.id !== id)
}


</script>

<template>
  <div class="container mx-auto">
<Header/>
<div class="mt-12 md:flex">

  <!-- en este componente (es un componente con un formulario) le estamos pasando el objeto que tenemos arriba como props  -->
  <!-- si lo quieres pasar para utilizar en un formulario debes usar la sintasis de: -->
   <!-- v-model:nombreDeclaradoParaElOtroComponente="objeto.valor" -->
  <Form class="  bg-slate-300 shadow-2xl rounded-xl py-10 px-5 mb-10"
  v-model:pet="formPacient.pet"
    v-model:propietary="formPacient.propietary"
    v-model:email="formPacient.email"
    v-model:symptoms="formPacient.symptoms"
   v-model:high="formPacient.high"
   :id="formPacient.id"
        @save-pacient="savePacient"
   />
   <div
   class="md:w-1/2 md:h-screen overflow-y-scroll" 
   >
  <h1
  class="font-black text-3xl uppercase text-center text-white mt-9" 
  >list pacient</h1>
<h1
class="w-1/2 ml-44 text-xl text-center text-black mt-9 bg-white"
 v-if="pacients.length<=0">non pacient</h1>
 <div v-else>
<EachPacient
v-for="pacient in pacients"
:key="pacient.id"
:pacient="pacient"
@up-date="update"
@deleted="deleted"
/>
 </div>
  </div>
</div>
  </div>
</template>


