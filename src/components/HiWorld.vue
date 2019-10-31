<template>
  <div class="hello">
    <h1>Une autre belle page Vue</h1>
    <h2>Message synchronisé: {{ message }}</h2>
    <input v-model="message" @input="storeMsgOnLocal" placeholder="Tapez le message à synchroniser">
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      message: this.$ls.get('sync_msg')
    }
  },
  methods: {
    storeMsgOnLocal() {
      this.$ls.set('sync_msg', this.message);
    }
  },
  mounted() {
    this.$ls.set('sync_msg', 'Default message');
    
    let callback = (val, oldVal, uri) => {
      this.message = this.$ls.get('sync_msg')
    } 
    
    this.$ls.on('sync_msg', callback)
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
