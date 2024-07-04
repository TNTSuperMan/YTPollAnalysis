<script setup>
import {ref,computed} from "vue"
import Option from './components/Option.vue'
const votecount = ref(0)
const polldata = ref([])
</script>
<template>
    <div class="box">
        <input type="text" class="title" placeholder="コミュニティに質問する..."><br>
        <label class="vc"><input type="number" min="0" v-model="votecount" class="vcinp">票</label>
        <Option v-for="(d,i) in polldata" v-model="polldata[i]" :id="i"
        :vc="votecount" @del="polldata.splice(i,1)"/>
        <br><button @click="polldata.push({name:'',rate:0})" class="add">選択肢をさらに追加</button>
    </div>
    <details>
        <summary>クレジット</summary>
        <table>
            <tr><td>コードエディタ</td><td><a target="_blank" href="https://code.visualstudio.com">Visual Studio Code</a></td></tr>
            <tr><td>フレームワーク</td><td><a target="_blank" href="https://vuejs.org">Vue</a></td></tr>
            <tr><td>コンパイラ</td><td><a target="_blank" href="https://vitejs.dev">Vite</a></td></tr>
            <tr><td>パッケージ管理</td><td><a target="_blank" href="https://www.npmjs.com">npm</a></td></tr>
            <tr><td>スタイル</td><td><a target="_blank" href="https://www.google.com">Google</a></td></tr>
        </table>
    </details>
</template>
<style scoped>
.title{
    border:none;
}
.vc{
    color:#aaa;
}
.vcinp{
    color:#aaa;
    border:none;
}
td{
    padding:3px;
}
td a{
    color:#0ff;
    text-decoration: none;
    transition:all 0.3s ease;
}
td a:hover{
    color:#00f;
    text-decoration: underline;
}
summary{
    cursor:pointer;
    user-select: none;
}
</style>
