        <script setup>
        const props = defineProps({
                    key: {
                        type: Number,
                        required:true
            },
                       pacient: {
                           type: Object,
                           required: true,
      }

        })

    defineEmits(['up-date',"deleted"])
        </script>

<template>
    
<div
class=" grid  md:grid-col-12  mx-5 my-10 bg-slate-300 shadow-xl px-5 py-10 rounded-xl"
>
    <p
    class="font-bold mb-3 text-black uppercase"
    >ID:{{ pacient.id }}
    <span class="font-normal normal-case"></span>
</p>
        <p
        class="font-bold mb-3 text-black uppercase"
        >Name pet:{{ pacient.pet }}
        <span class="font-normal normal-case">
           
        </span>
    </p>

        <p
        class="font-bold mb-3 text-black uppercase"
        >Name propietary:{{ pacient.propietary }}
        <span class="font-normal normal-case"></span>
    </p>

        <p
        class="font-bold mb-3 text-black uppercase"
        >Email:{{ pacient.email }}
        <span class="font-normal normal-case"></span>
    </p>

        <p
        class="font-bold mb-3 text-black uppercase"
        >High date:{{ pacient.high }}
        <span class="font-normal normal-case"></span>
    </p>
          <p
            class="font-bold mb-3 text-black uppercase"
            >Symptoms:{{ pacient.symptoms }}
            <span class="font-normal normal-case"></span>
        </p>
        <div class="d-flex  flex-row gap-5 mt-10">

            <button
            type="button"
            class=" w-1/2  py-2  bg-orange-400 hover:bg-orange-500 duration-500 text-white
            uppercase rounded-lg font-bold"
            @click="$emit('up-date', pacient.id)"
            >edit</button>

                        <button
                        type="button"
                           class=" w-1/2 py-2  bg-red-700 hover:bg-red-800 duration-500 text-white
                           uppercase rounded-lg font-bold"
                           @click="$emit('deleted',pacient.id)"
                        > deleted</button>

        </div>

</div>
    
</template>


