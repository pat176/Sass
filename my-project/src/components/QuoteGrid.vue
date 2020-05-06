<template>
  <div class="row">
      <Quote v-for="(quote, index) in quotes" :key="index + 1" @click.native="removeQuote(index)">{{ index + 1 }}. {{ quote }}</Quote>
  </div>
</template>

<script>
import Quote from './Quotes.vue'
export default {
  props: {
    quotes: Array
  },
  components: {
    Quote
  },
  methods: {
    removeQuote (id) {
      this.$emit('remQuote', id)
    }
  }

}
</script>

<style>

</style>
