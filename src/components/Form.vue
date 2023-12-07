        <script setup>
import { reactive,computed } from "vue";
import Alert from "./Alert.vue";

//hacemos lo mismo que en app colocamos el objeto que usaremos en un componente mas abjo aqui por que esta 
// en una posicion mas alta
        const alert = reactive({
                    message: "",
                    type:"",
            
                })
        //aparte de eventoso funciones podemos pasarle por define emits valores de un objeto de un form
        //simplemente ponemos update:pet
        //el valor es el que pusimos en el padre mediante el v-model:pet="objeto.pet"
                //ahora tenemos que emitir como sabemos de las funciones o eventos pues debemos pasarle
                //en que input colocamos cada valor
        //---> esto va en cada input por su valor @input="$emit('update:pet',$event.target.value)"
        //y tenemos que ponerle el valor para pasarlo al padre :value="pet"
        //Nota esto es asi y hay que saberlo tal como es 
        //IMPORTANTE es buena practica colocar los objetos o datos reactivo importantes en el padre y asi
        // IMPORTANTE poder pasarlos con mayor facilidad
                
// acabamos de darle un valor a este define emit para usarlo dentro del script
     const emit= defineEmits(['update:pet', 'update:propietary', 'update:email',
            'update:symptoms', 'update:high', 'save-pacient'])

//tenemos que pasar las props para mandar el objeto al padre
        const props = defineProps({

          // creamos un id y debemos pasarle la propr de esta forma ya que en el componente padre lo declaramos como null
                  id: {
                    type: [String,null],
            required:true,
          },

                    pet: {
                        type: String,
                        required: true
                    },
                    propietary: {
                      type: String,
                      required: true
                  },
                  email: {
                    type: String,
                    required: true
                },
                symptoms: {
                  type: String,
                  required: true
              },
                      high: {
                type: String,
                required: true
            },
    
                })

        const send = () => {
            // e.preventDefault() esto es lo mismo que eliminar esto y quitar la e de call back 
            // y colocarlo en el mismo formulario en este caso en @submit.prevent
            //con esto prevenimos que se refresque la pagina y se borre la informacion
                    //y debemos pasarle en values las props 

            if (Object.values(props).includes("")) {
                alert.message = "campos obligatorios"
                alert.type = "error"
                return

                  } 
                  // llamamos una funcion emit dentro de otra y la llamamos como declaramos el defineemit que esta arriba
          emit('save-pacient')

                  alert.message = 'pacient ok'
                  alert.type = 'ok'
                  setTimeout(() => {
            
              alert.message= ""
              alert.type= ""

          
               },3000)
          
        }
        const edit = computed(()=>{
          return props.id
        })
        
        </script>



<template>
    <div class="md:w-1/2">

        <h1 class="font-black text-3xl text-center">FORM</h1>
        <p class="text-lg mt-5 text-center mb-10">Patient
            <br>
        <span class="text-orange-300 font-bold">add</span>
        </p>
        <Alert
        v-if="alert.message"
        :alert="alert"/>
          <form
      class="bg-slate-300 py-10 px-5 mb-10" 
      @submit.prevent="send">

    <div class="mb-5">

      <label
      class="block uppercase font-bold "
      for="pet">
        Name pet
      </label>
      <input
      class="w-full p-2 mt-2 rounded-lg "
      id="pet"
       type="text"
       placeholder="name pet"
       :value="pet"
       @input="$emit('update:pet', $event.target.value)"
       >
       
    </div>
        <div class="mb-5">
          <label
          class="block uppercase font-bold "
          for="propietary">
            Name propietary
          </label>
          <input
           class="w-full p-2 mt-2 rounded-lg "
          id="propietary"
           type="text"
           placeholder="name propietary"
            :value="propietary"
          @input="$emit('update:propietary',$event.target.value)"
            >
       
        </div>
               <div class="mb-5">
              <label
              class="block uppercase font-bold "
              for="propietary">
                email
              </label>
              <input
               class="w-full p-2 mt-2 rounded-lg "
              id="email"
               type="email"
               placeholder="email"
             :value="email"
            @input="$emit('update:email', $event.target.value)"

                 >
       
            </div>
                 <div class="mb-5">
                  <label
                  class="block uppercase font-bold "
                  for="high">
                   High date
                  </label>
                  <input
                   class="w-full p-2 mt-2 rounded-lg"
                  id="high"
                   type="date"
                   :value="high"
                 @input="$emit('update:high', $event.target.value)"
                   >
                   <div class="mb-5">
                <label
                class="block uppercase font-bold "
                for="symptoms">
                  Symptoms
                </label>
                <textarea
                 class="w-full p-2 mt-2 rounded-lg "
                id="symptoms"
                 placeholder=" write symptoms"
                 :value="symptoms"
               @input="$emit('update:symptoms', $event.target.value)"
                  />
              </div>
                </div>
                <button
                type="submit"
                class="bg-orange-400 w-full p-3 text-white uppercase font-bold
                 hover:bg-orange-600 transition-colors duration-500 cursor-pointer rounded-lg"
                 :value="[edit?'save update':'register']"
                > register pet</button>

      </form>

    </div>
</template>



