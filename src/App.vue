<script setup>
import {ref,computed} from "vue"
import Option from './components/Option.vue'
const votecount = ref(0)
const polldata = ref([])
const state = computed(()=>{
    if(polldata.value.length == 0){
        return "選択肢がありません"
    }
    let per = 0
    polldata.value.forEach(e=>per+=e.rate)
    if(per != 100){
        return "割合の合計が100%ではありません"
    }
    let sum = 0
    polldata.value.forEach(e=>
        sum += Math.round(votecount.value * (e.rate / 100))
    )
    if(sum == votecount.value){
        return "結果は正しいです"
    }else{
        return "結果は誤差があります"
    }
})
</script>
<template>
    人数： <input type="number" min="0" v-model="votecount">
    <Option v-for="(d,i) in polldata" v-model="polldata[i]" :id="i"
        :vc="votecount" @del="polldata.splice(i,1)"/>
    <br><button @click="polldata.push({name:'',rate:0})">選択肢をさらに追加</button>
    <p>{{ state }}</p>
</template>