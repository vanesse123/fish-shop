<script setup>
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import CategoryNav from './components/CategoryNav.vue'
import Banner from './components/Banner.vue'
import ProductList from './components/ProductList.vue'
import SaleSection from './components/SaleSection.vue'
import ProductDetail from './components/ProductDetail.vue'

const selectedCategory = ref('全部商品')
const searchKeyword = ref('')
const selectedProduct = ref(null)
const cart = ref([])

function searchProducts(keyword){
  searchKeyword.value = keyword.trim()
}

function showProductDetail(product){
  selectedProduct.value = product
}

function backToProducts() {
  selectedProduct.value = null
}

function addToCart(item) {
  const existingItem = cart.value.find(
    cartItem => cartItem.product.id === item.product.id
  )

  if(existingItem) {
    existingItem.quantity += item.quantity
  } else {
    cart.value.push(item)
  }

  console.log('目前購物車:',cart.value)
}
</script>

<template>
  <ProductDetail 
    v-if="selectedProduct"
    :product="selectedProduct"
    @back="backToProducts"
    @add-to-cart="addToCart"
  />
  <template v-else>
    <Navbar @search="searchProducts" />

    <Banner />

    <CategoryNav 
      :selected-category="selectedCategory"
      @change-category="selectedCategory = $event"
    />

    <ProductList 
      :selected-category="selectedCategory"
      :search-keyword="searchKeyword"
      @select-product="showProductDetail"
    />

    <SaleSection />
  </template>
</template>
