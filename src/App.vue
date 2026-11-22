<script setup>
import { ref,watch } from 'vue'
import Navbar from './components/Navbar.vue'
import CategoryNav from './components/CategoryNav.vue'
import Banner from './components/Banner.vue'
import ProductList from './components/ProductList.vue'
import SaleSection from './components/SaleSection.vue'
import ProductDetail from './components/ProductDetail.vue'
import Cart from './components/Cart.vue'

const selectedCategory = ref('全部商品')
const searchKeyword = ref('')
const selectedProduct = ref(null)

const savedCart = localStorage.getItem('cart')
const cart = ref(savedCart ? JSON.parse(savedCart) : [])
const showCart = ref(false)
watch(
  cart,
  (newCart) => {
    localStorage.setItem('cart', JSON.stringify(newCart))
  },
  { deep: true}
)


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

function opencart() {
  showCart.value = true
}

function closecart() {
  showCart.value = false
  selectedProduct.value = null
}

function updateCartQuantity(productId,change) {
  const item = cart.value.find(
    cartItem => cartItem.product.id === productId
  )

  if (item) {
    item.quantity = Math.max(1,item.quantity + change)
  }
}

function removeCartItem(productId) {
  cart.value = cart.value.filter(
    item => item.product.id !== productId
  )
}
</script>

<template>
  <Cart
    v-if="showCart"
    :cart="cart"
    @back="closecart"
    @update-quantity="updateCartQuantity"
    @remove-item="removeCartItem"
  />

  <ProductDetail 
    v-else-if="selectedProduct"
    :product="selectedProduct"
    @back="backToProducts"
    @add-to-cart="addToCart"
    @open-cart="opencart"
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
