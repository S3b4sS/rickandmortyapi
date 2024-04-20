<template>
    <div class="flex flex-col overflow-hidden rounded-xl shadow-xl">
        <div>
            <img :src="character.image" alt="desactiva el bloqueador de anuncios para ver las mujeres tetonas" class="p-9 bg-white ">

        </div>

        <div class="p-9 bg-blue-200 h-full flex justify-center items-center text-2xl" >
            <h3>{{character.name}}</h3>

        </div>

    </div>


</template>

<script setup>

import { defineProps } from 'vue';
import { Icon } from '@iconify/vue';

    const props = defineProps({

    character:{
        required: true,
        type: Object
        }
        
    }) 

</script>