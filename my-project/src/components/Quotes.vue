<template>
  <div class="col-sm-6 col-md-4 col-lg-3">
    <div class="card">
      <div class="card-body quote">
        <slot></slot>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['quote']

}
</script>

<style>
  .card {
    margin: 10px;
  }
  .card-body {
    font-family: 'Arizonia', cursive;
    color: #6e6e6e;
    font-size: 24px;
  }
  .quote:hover {
    background: #ffe6e6;
    cursor: pointer;
  }
</style>
