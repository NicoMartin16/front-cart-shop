<template>
  <button @click="changeButton" v-if="showAddCart" class="product-container__list-item-button">
    <img src="/src/assets/images/icon-add-to-cart.svg" /> Add to cart
  </button>
  <button v-else class="product-container__list-item-button-add-cart">
    <img
      @click="decrement"
      class="decrement"
      src="/src/assets/images/icon-decrement-quantity.svg"
      alt="decrement"
    />
    <span>{{ quantity }}</span>
    <img
      @click="increment"
      class="increment"
      src="/src/assets/images/icon-increment-quantity.svg"
      alt="increment"
    />
  </button>
</template>
<script lang="ts" setup>
import { ref } from 'vue'

const showAddCart = ref(true)
const quantity = ref(1)

const emits = defineEmits<{
  (e: 'onChangeQuantity', quantity: number): void
}>()

const changeButton = () => {
  showAddCart.value = !showAddCart.value
  emits('onChangeQuantity', quantity.value)
}

const increment = () => {
  quantity.value++
  emits('onChangeQuantity', quantity.value)
}

const decrement = () => {
  if (quantity.value > 1) {
    quantity.value--
    emits('onChangeQuantity', quantity.value)
  } else {
    showAddCart.value = !showAddCart.value
  }
}
</script>
<style lang="sass" scoped>
.product-container__list-item-button
      cursor: pointer
      position: relative
      background-color: #FAFAFA
      z-index: 1
      top: -20px
      left: 25%
      display: flex
      justify-content: center
      align-items: center
      width: 50%
      padding: 10px
      border-radius: 20px
      font-size: 16px
      gap: 10px
      color: hsl(14, 65%, 9%)
      border: 1px solid hsl(7, 20%, 60%)
.product-container__list-item-button-add-cart
    position: relative
    background-color: hsl(14, 86%, 42%)
    z-index: 1
    top: -20px
    left: 25%
    display: flex
    justify-content: space-between
    align-items: center
    width: 50%
    padding: 10px
    border-radius: 20px
    font-size: 20px
    border: 1px solid hsl(14, 86%, 42%)
    color: #FAFAFA
    .decrement,
    .increment
        width: 20px
        height: 20px
        cursor: pointer
        border-radius: 50%
        padding: 5px
        border: 1px solid #FAFAFA
        img
            width: 100%
            height: 100%
</style>
