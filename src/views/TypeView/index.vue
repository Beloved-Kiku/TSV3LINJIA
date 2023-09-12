<template>
    <!-- 顶部搜索栏部分 -->
    <van-search shape="round" placeholder="请输入搜索关键词" />
    <div class="main">
        <!-- 左边侧边栏部分 -->
        <van-sidebar class="left" v-model="nowActive">
             <van-sidebar-item
             @click="filterGoods(type.name,MockData.types)"
              v-for="(type) in MockData?.types" :key="type.id" :title="type.name"
             />
        </van-sidebar>
        <!-- 右边内容部分 -->
        <van-list class="right" finished-text="没有更多了">
            <div class="good" v-for="goods in TemplateMockData[0].products" :key="goods.id">
                <!-- 商品图片 -->
                <img class="img" :src="goods.banner" alt="" />
                <!-- 商品名字 -->
                <p class="name">{{ goods.name }}</p>
                <!-- 商品价格 -->
                <p class="price">￥{{ goods.price }}元</p>
                <!-- 商品规格 -->
                <p class="specs">{{ goods.specs }}</p>
                <van-button round type:string="info" color="linear-gradient(to right, #ff6034, #ee0a24)">
                    加入购物车
                </van-button>
            </div>
        </van-list>
    </div>
</template>

<script setup lang="ts">
import {ref,onMounted} from 'vue'
let MockData:any = ref("")
let TemplateMockData: any = ref("")
let nowActive = ref(0)
const filterGoods = (type: any, MockTypes: any) => {
    let newArray:any =ref([])   
     nowActive.value = type.id 
    TemplateMockData.value = MockTypes?.forEach(item=>{        
        if(item.name ==type){
            newArray.value.push(item)
        }
    })  
     TemplateMockData.value = newArray.value     
}
MockData.value = JSON.parse(window.localStorage.getItem('MockData') as string)
filterGoods(MockData.value.types[0].name, MockData.value.types)

 
</script>

<style scoped>
.main {
    display: flex;
}

.left {
    width: 26.667vw;
}

.right {
    flex: 1;
    height: 90vh;
    overflow: scroll;
}

.good {
    width: 80%;
    margin: 0 auto;
    background-color: #fff;
    border-radius: 4vw;
    padding: 4vw;
    margin-bottom: 2.667vw;
}

.good>.supplier {
    font-size: 5.067vw;
    text-align: center;
}

.good>img {
    width: 100%;
    border-radius: 4vw;
}

.good>.specs {
    font-size: 5.333vw;

    margin: 4vw 0;
}

.good>.price {
    font-size: 5.333vw;
    color: red;
    font-weight: bold;
    margin: 4vw 0;
}

.good>.Btn {
    width: 100%;
    border-radius: 8vw;
}
</style>
