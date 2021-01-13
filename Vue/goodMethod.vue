<template>
  <div>
    <!-- 为了过滤数组中的元素，很容易将v-if与v-for在同个元素同时使用。 -->
    <div v-for='(product,index) in products' v-if='product.price < 500' :key="index"></div>
    <!-- 问题是在 Vue 优先使用v-for指令，而不是v-if指令。它循环遍历每个元素，然后检查v-if条件。
    这意味着，即使我们只想渲染列表中的几个元素，也必须遍历整个数组-->
   <!--  this.products.map(function (product) {
      if (product.price < 500) {
        return product
      }
    }) -->
    <div v-for='(product,index) in cheapProducts' :key="index"></div>
  </div>
</template>

<script>
export default {
  name: 'goodMethod',
  data() {
    products: ''
  },
  computed: {
    //一个更聪明的解决方案是遍历一个计算属性，
    cheapProducts: () => {
      return this.products.filter(function (product) {
        return product.price < 100
      })
    }
  },
  methods: {
    
  },
}
</script>