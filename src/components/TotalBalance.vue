<template>
  <div class="total-value" 
    :class="totalClass"
    >Balance: {{total}}
  </div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    },
  },
  computed: {
    totalClass() {
      if (this.total > 0) {
        return 'total-positive'
      }

      if (this.total < 0) {
        return 'total-negative'
      }

      return ''
    }
  }
}
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
  color: #000;
}

.total-positive {
  color: green;
}

.total-negative {
  color: red
}
</style>