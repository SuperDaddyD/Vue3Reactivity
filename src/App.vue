<script setup>
import {ref, unref,isRef, reactive,toRefs, onMounted} from "vue"
let count = ref(1);
function double(){
    //UNREF WILL DISPLAY ANY REF OR VARIABLE VALUE!!
    //EVEN IF YOU DONT DO EX count.value
    //BASICALLY DONT HVE TO USE '.vaule property'
    //YOU CAN DO unref(count) and it will show the value asif count.value!!
    count.value = unref(count) * 2

    //isRef is like a check to see if variable is a ref in the
    //first place. You can use it to check example
    const check = isRef(count) ? count.value : count;
    console.log(check)
}

//ANOTHER WAY TO USE ref TO GRAB DOM ELEMENTS AND MANIPULATE
//MUST BE WRAPPED IN "onMount" OR WILL NOT WORK!!!
const button = ref("")

onMounted(()=>{
    console.log(button.value)
})

//REACTIVE WILL RETURN A REF AKA STATE OBJECT THAT
//YOU CAN REFERENCE IN DOM, PLUS IT IS BEING TRACKED AS STATE!!!
//BETTER TO USE THAN ref IF YOU HAVE A LOT OF STATE TO TRACK
const cube = reactive({
        height:10,
        width:20,
        length:200
    })

//toRefs IS GREAT!! YOU CAN REFERENCE YOUR REACTIVE OBJECT
//SO NOW YOU DO NOT HAVE TO DO cube.height,etc 
//JUST {{height}}
//FULL OF YOUR STATE AND DO THIS  
const {height, width,length} = toRefs(cube)

</script>

<template>
  <div>
    <h1>{{ count }}</h1>

    <button ref="button" @click="double">Click</button>

    <h3>Hello World REACTIVE</h3>
    {{ cube.height }}
    {{ cube.width }}
    {{ cube.length }}
    <h3>Hello World toRefs even Better!!</h3>
    {{ height }}
    {{ width }}
    {{ length }}
  </div>
</template>

<style scoped>
</style>
