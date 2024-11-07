<template>
  <div class="summary-cart-container">
    <h1 class="summary-cart-container__title">Your Cart({{ getTotalItems(productsOnCart) }})</h1>
    <div v-if="productsOnCart.length !== 0">
      <div
        class="summary-cart-container__item"
        v-for="(product, index) in productsOnCart"
        :key="index"
      >
        <div class="summary-cart-container__item-description">
          <p class="title">{{ product.name }}</p>
          <p class="quantity">{{ product.quantity }}x</p>
          <p class="unit-price">@${{ product.price }}</p>
          <p class="total-price">${{ product.price * (product.quantity ?? 0) }}</p>
        </div>
        <div class="summary-cart-container__item-delete-action">
          <img src="/src/assets/images/icon-remove-item.svg" alt="remove image" />
        </div>
      </div>
      <div class="summary-cart-container__price">
        <p class="total-title">Order total</p>
        <p class="price">${{ getTotalBill(productsOnCart) }}</p>
      </div>
      <div class="summary-cart-container__message">
        <img src="/src/assets/images/icon-carbon-neutral.svg" alt="carbon neutral" />
        <p>This is a <b>carbon-neutral</b> delivery</p>
      </div>
      <button class="summary-cart-container__button">Confirm order</button>
    </div>
    <div v-else>
      <div class="container-empty-cart">
        <img src="/src/assets/images/illustration-empty-cart.svg" alt="empty cart" />
        <p>Your added items will appear here</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { Product } from '@/interfaces/product.model'

const props = defineProps<{
  productsOnCart: Product[]
}>()

const getTotalBill = (products: Product[]): number => {
  return products.reduce((acc, product) => {
    return acc + product.price * (product.quantity ?? 0)
  }, 0)
}

const getTotalItems = (products: Product[]): number => {
  return products.reduce((acc, product) => {
    return acc + (product.quantity ?? 0)
  }, 0)
}

console.log(props.productsOnCart)
</script>

<style lang="sass" src="./summarycart.sass" scoped></style>
