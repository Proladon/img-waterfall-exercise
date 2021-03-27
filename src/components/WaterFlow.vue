<template>
  This is Water Flow
  <!-- {{img.source}} -->
  <!-- <img v-for="img in img.source" :key="img" :src="img" alt=""> -->
  <!-- <img :src="a" alt=""> -->
</template>

<script setup>
import { onMounted, reactive } from "vue";

const column = 5
const columnWidth = 200
const gap = 10
const columnIndex = []

// all img file path
const img = reactive({
    source:[]
})

const waterflow = ()=>{
    // init column
    for(let i=0; i<column; i++){
        columnIndex.push({top:0, left: i*columnWidth})
    }

    for(let i=1; i<img.source.length; i++){
        let imgItem = new Image()
        imgItem.src = img.source[i]
        imgItem.width = columnWidth
        imgItem.style.position = "absolute"



        if(i<=5){
            // create img
            imgItem.onload = imgItem.onerror = (e)=>{
                imgItem.style.top = columnIndex[i-1].top + 'px'
                
                imgItem.style.left = columnIndex[i-1].left + 'px'
                
                columnIndex[i-1].top = imgItem.height + gap
            }
        }
        else{
            imgItem.onload = imgItem.onerror = (e)=>{
                const temp = []
                for(let column of columnIndex){
                    temp.push(column.top)
                }
                const minColumn = Math.min.apply(null, temp)
                const min = temp.indexOf(minColumn)

                imgItem.style.top = columnIndex[min].top + 'px'
                imgItem.style.left = columnIndex[min].left + 'px'

                columnIndex[min].top = imgItem.height + gap

            }
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