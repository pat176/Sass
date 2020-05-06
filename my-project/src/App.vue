<template>
  <div class="container">
    <div class="progress my-3">
      <div class="progress-bar" role="progressbar" :style="styleObject" :aria-valuenow="width" aria-valuemin="0" aria-valuemax="100">
        <span v-if="quotes.length > 0">
          {{ quotes.length }} / 10
        </span>
      </div>
    </div>
    <div class="input-group my-3">
      <input type="text" class="form-control" placeholder="Add Quote" aria-label="Add Quote" aria-describedby="basic-addon2" v-model="value">
      <div class="input-group-append">
        <button class="btn btn-outline-secondary" type="button" @click="addQuote">Button</button>
      </div>
    </div>
    <quote-grid :quotes="quotes" @remQuote="remove"></quote-grid>
    <div class="row">
      <div class="col-sm-12 text-center">
        <div class="alert alert-info">Tip: You Can Click On The Quote To Delete It!</div>
      </div>
    </div>
  </div>
</template>

<script>
import QuoteGrid from './components/QuoteGrid.vue'
export default {
  data: function () {
    return {
      quotes: [],
      maxQuotes: 10,
      value: '',
      width: 0,
      styleObject: {
        width: 0
      }
    }
  },
  methods: {
    addQuote () {
      if (this.value.length > 0) {
        if (this.maxLength) {
          this.quotes.unshift(this.value)
          this.value = ''
          this.width += 10
          this.styleObject.width = this.width + '%'
          if (localStorage.quotes) {
            localStorage.quotes = JSON.stringify(this.quotes)
          } else {
            localStorage.setItem('quotes', JSON.stringify(this.quotes))
          }
        } else {
          alert('You Have Already Added 10 Quotes Delete Some Of Them To Add More')
          this.value = ''
        }
      } else {
        alert('Please Enter A Valid Quote')
      }
    },
    remove (index) {
      this.quotes.splice(index, 1)
      this.width -= 10
      this.styleObject.width = this.width + '%'
      if (localStorage.quotes) {
        localStorage.quotes = JSON.stringify(this.quotes)
      } else {
        localStorage.setItem('quotes', JSON.stringify(this.quotes))
      }
    }
  },
  computed: {
    maxLength () {
      if (this.quotes.length === this.maxQuotes) {
        return false
      } else {
        return true
      }
    }

  },
  components: {
    quoteGrid: QuoteGrid

  },
  mounted () {
    if (localStorage.quotes) {
      this.quotes = JSON.parse(localStorage.quotes)
      this.width = this.quotes.length * 10
      this.styleObject.width = this.width + '%'
    }
  }
}
</script>
<style>
  .progress {
    height: 30px;
  }
</style>
