<template>
  <div class="app">
    <NavBar :categories="categories" @selected="selectedCategory"/>
    <List :products="products" @add-to-cart="addToCart"/>
    <Cart :cart="cartList" @remove-cart-id="removeCart" @clear-cart="clearCart"/>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { products,categories } from "./assets/products.js"
import Cart from "./components/Cart.vue";
import List from "./components/List.vue";
import NavBar from './components/NavBar.vue';
console.log(categories)

//장바구니 상태
const cartList = ref([]);

const addToCart = (list) => {
  //1. list가 된 내용이 cart에 있는지 없는지 확인
  const findItem = cartList.value.find((item)=>{
    return item.id === list.id;
  });
  // console.log(findItem)
  //2. 있으면 수량을 하나 증가
  if(findItem){
    findItem.count += 1;
  } else {
  //3. 없으면 cart에 추가, 수량1개로저장
  cartList.value.push({...list, count:1});
  }
}
const removeCart = (cartID) => {
    //cartList 항목이 새로 생성 : cartID가 없는 데이터로.
    cartList.value = cartList.value.filter((item)=>{
      return item.id !== cartID;
    });
  }
const clearCart = (value) => {
  if(value){
    cartList.value = [];
  }
}
const selectedCategory = (item) => {

}

</script>

<style lang="scss" scoped>

</style>