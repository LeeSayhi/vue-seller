<template>
    <!-- <router-view></router-view> -->
    <v-header :seller="seller"></v-header> 
</template>

<script>
  import header from './components/header/header.vue'

  export default {
    data () {
      return {
        seller: {}
      }
    },
    components: {
      'v-header': header
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        if (response.data.errno === 0) {
          this.seller = Object.assign({}, this.seller, response.data.data)
        }
      })
    }
  }
</script>

<style>

</style>
