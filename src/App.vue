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

function searchProducts(keyword){
  searchKeyword.value = keyword.trim()
}

function showProductDetail(product){
  selectedProduct.value = product
}

function backToProducts() {
  selectedProduct.value = null
}
</script>

<template>
  <ProductDetail 
    v-if="selectedProduct"
    :product="selectedProduct"
    @back="backToProducts"
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
