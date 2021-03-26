<template>
  This is Water Flow
  <!-- {{img.source}} -->
  <!-- <img v-for="img in img.source" :key="img" :src="img" alt=""> -->
  <!-- <img :src="a" alt=""> -->
</template>

<script setup>
import { onMounted, reactive } from "vue";

// all img file path
const img = reactive({
    source:[]
})

const waterflow = ()=>{
    const containerWidth = 1000
    const imgWidth = 200
    const gap = 10

    

    for(let i=1; i<img.source.length; i++){
        let imgItem = new Image()
        imgItem.src = img.source[i]
        imgItem.width = imgWidth
        imgItem.onload = imgItem.onerror = (e)=>{
            // get img info
            

        }
        document.body.appendChild(imgItem)

    }

}

onMounted(()=>{
    
    // get all img file path & store in img.source
    for(let num=1; num<13; num++){
        let filePath = `/src/assets/img (${num}).jpg`
        img.source.push(filePath)
    }

    waterflow()

})

</script>

<style>
</style>