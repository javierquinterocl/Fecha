<script setup>
import { ref } from 'vue'

const array = ref([
  { name: 'Arroz', Price: 2000, Cant: 2, Venc: 4 },
  { name: 'Pescado', Price: 1000, Cant: 4, Venc: 1 },
  { name: 'Leche', Price: 2000, Cant: 0, Venc: 0 },
  { name: 'Huevos', Price: 2000, Cant: 0, Venc: 1 }
])
let total = ref(0)
let pricetotal = ref(0)
function verifica() {
  array.value.forEach((e) => {
    if (e.Cant === 0) {
      e.Price = 0
      e.Cant = 0
    }
    if (e.Venc === 0) {
      e.Price = 0
      e.Cant = 0
    }
  })
}
verifica()
function vencimiento() {
  array.value.forEach((e) => {
    total.value += e.Cant
    pricetotal.value += e.Price
  })
}

vencimiento()
</script>

<template>
  <div class="container">
    <div class="data">
      <div class="productone">
        <span>Producto: </span>
        <div
          v-for="(product, index) in array"
          :key="index"
          class="product1"
          v-show="product.Cant != 0 && product.Venc != 0"
        >
          {{ product.name }}
        </div>
      </div>
      <div class="price">
        <span>Precios: </span>
        <div
          v-for="(product, index) in array"
          :key="index"
          class="product2"
          v-show="product.Cant != 0 && product.Venc != 0"
        >
          {{ product.Price }}
        </div>
      </div>
      <div class="cant">
        <span>Cant: </span>
        <div
          v-for="(product, index) in array"
          :key="index"
          class="product3"
          v-show="product.Cant != 0 && product.Venc != 0"
        >
          {{ product.Cant }}
        </div>
      </div>
      <div class="venc">
        <span>Dias: </span>
        <div
          v-for="(product, index) in array"
          :key="index"
          class="product4"
          v-show="product.Cant != 0 && product.Venc != 0"
        >
          <span class="" v-if="product.Venc >= 1" :class="red">{{ product.Venc }} <span v-show="product.Venc <=1" class="red">F</span></span>
        </div>
      </div>
    </div>
    <div class="method"><span>La cantidad de productos es :</span>{{ total }}</div>
    <div class="method"><span>El precio de todos los productos es :</span>{{ pricetotal }}</div>
  </div>
</template>

<style scoped>
.red {
  color: rgb(255, 70, 70);
}
.product1 {
  display: flex;
  justify-content: space-between;
}
.product3 {
  display: flex;
  justify-content: space-between;
}
.product2 {
  display: flex;
  justify-content: space-between;
}
.product4 {
  display: flex;
  justify-content: space-between;
}

.productone,
.price,
.cant,
.venc {
  display: flex;
  justify-content: space-between;
}
.data {
  max-width: 400px;
}
</style>
