<script setup>
import {ref,watch} from "vue"
const props = defineProps(["vc","id"])
const model = defineModel()
const prov_rate = ref(model.value.rate)
watch(prov_rate,e=>{
  if(prov_rate.value > 100){
    prov_rate.value = 100
  }
  model.value.rate = prov_rate.value
})
</script>
<template>
  <div class="item" :id="props.id">
    <button @click="$emit('del')">X</button>
    <div class="text">
      <div class="bar" :style="'width:' + model.rate + '%'"></div>
      <input type="text" v-model="model.name" placeholder="選択肢を追加">
    </div>
    &nbsp;&nbsp;&nbsp;
    <input type="number" min="0" max="100" v-model="prov_rate">%
    ({{ Math.round(props.vc * (model.rate / 100)) }})
  </div>
</template>
<style scoped>
input[type=text]{
  width:100%;
  height:15px;
  position:relative;
}
div.bar{
  transition:all 0.3s ease;
  display:inline-block;
  position:absolute;
  background:rgba(255,255,255,0.5);
  height:26px;
  top:2px;
  left:2px;
  border-radius: 5px;
}
div.text{
  position:relative;
  display:inline-block;
  width:calc(100% - 300px);
}
</style>