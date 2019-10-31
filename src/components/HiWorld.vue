<template>
  <div class="hello">
    <h1>Une autre belle page Vue</h1>
    <h2>{{ message }}</h2>
    <input v-model="message" @input="storeOnLocal" placeholder="modifiez-moi">
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      message: this.$ls.get('msg')
    }
  },
  methods: {
    storeOnLocal() {
      this.$ls.set('msg', this.message);
    }
  },
  mounted() {
    this.$ls.set('msg', 'boo');
    
    let callback = (val, oldVal, uri) => {
      this.message = this.$ls.get('msg')
    } 
    
    this.$ls.on('msg', callback)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  background-color: aquamarine;
}
</style>
