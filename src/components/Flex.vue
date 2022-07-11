<template>
  <div class="container">

    <div class="box">
      <div class="item" v-for="item in state.list" :key="item.id">
        <img class="icon" :src="item.src" alt="" v-show="item.src">
        <p class="title" v-show="item.title">{{item.title}}</p>
      </div>
    </div>


  </div>
</template>



<script setup>
import { reactive, onMounted } from 'vue'
import CloneDeep from 'lodash.clonedeep'
import ResData from '@/mock/mockData.js'

//data
const state = reactive({
  list: []
})

//lifes
onMounted(() => {
  getList()
})

//function

/**
 * @description: 模拟请求，获取sku数据
 */
const getList = () => {
  let list = CloneDeep(ResData)
  state.list = calc(list, 5)
}


/**
 * @description: 计算
 * @param {Array} list: 列表
 * @param {Number} colNum: 每行展示的数量
 */
const calc = (list = [], colNum = 0) => {
  if (!list || list.length === 0 || !colNum) return []

  let temp = CloneDeep(list)
  const temp_len = temp.length
  const empty_num = colNum - (temp_len % colNum)  //需要填补的空元素数量
  if (+empty_num === 0) return temp
  for (let i = 0; i < empty_num; i++){
    temp.push({})
  }
  return temp
}



</script>

<style lang="less" scoped>
.container{
  width: 100%;
  height: 100vh;
  background-color: #dcdcdc;
  padding: 50px 20px;
}

.box{
  width: 100%;
  height: auto;
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: space-between;
}

.item{
  width: 130px;
  .icon{
    display: block;
    width: 80px;
    height: 80px;
    margin: 0 auto;
  }

  .title{
    color: #999;
    margin-top: 10px;
    text-align: center;
    font-size: 24px;
  }
}


</style>