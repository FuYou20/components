<script setup>
import card_plus from './components/prop_cardPlus_store.vue'
import card from './components/prop_card_store.vue';
</script>

<template>
  <div class="show">
    <card prop_name="blue的道具" :star_number=5 :coin_number=500 state="可兑换" state_text="3/3" :afford=true></card>
    <card prop_name="blue的道具" :star_number=5 :coin_number=500 state="已售空" state_text="3/3" :afford=true></card>
    <card prop_name="blue的道具" :star_number=5 :coin_number=500 state="可兑换" state_text="3/3" :afford=false></card>
    <card_plus prop_name='原神的祝福' 
    :amount=100 :star_number=5 :coin_number=3 
    description="来自提瓦特大陆的神秘力量" remark="原神之力" :onButtonClick="sayHello"></card_plus>
  </div>
 
</template>

<style scoped>
.show{
  display: flex;
  height: 100%;
  align-items: center; /* 垂直居中 */
  justify-content: space-around; /* 水平间隔 */
}
</style>
<script>
const sayHello =()=>{
  alert('hello')
}
</script>
