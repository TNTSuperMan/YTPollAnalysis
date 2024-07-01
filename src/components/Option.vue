<script setup>
import {computed} from "vue"
const props = defineProps(["vc","id"])
const model = defineModel()
</script>
<template>
  <div class="item" :id="props.id">
    <button @click="$emit('del')">X</button>
    <input type="text" v-model="model.name" placeholder="選択肢を追加">&nbsp;&nbsp;&nbsp;
    <input type="number" min="0" max="100" v-model="model.rate">%
    ({{ Math.round(props.vc * (model.rate / 100)) }})
  </div>
</template>
<style scoped>
input{
  border:none;
  border-radius: 0px;
  border-bottom:1px #666 solid;
  outline:none;
  transition:all 0.3s ease;
}
input:focus-visible{
  border-bottom:1px #fff solid;
}
input[type=number]{
  width:50px;
}
</style>