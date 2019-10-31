<template>
  <div class="hello">
    <h1>Une belle page Vue</h1>
    <h2>Message synchronisé: {{ msg }}</h2>
    <input v-model="msg" @input="storeMsgOnLocal" placeholder="Tapez le message à synchroniser">
    <section>
      <h3>Synchroniser les autres pages</h3>
      <input type="radio" v-model="sync" @change="storeMsgOnLocal" value="1">Oui
      <input type="radio" v-model="sync" value="0">Non
    </section>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: this.$ls.get('sync_msg'),
      sync: "1"
    }
  },
  methods: {
    storeMsgOnLocal() { 
      if(this.sync === "1") {
        this.$ls.set('sync_msg', this.msg);
      }
    }
  },
  mounted() {
    this.$ls.set('sync_msg', 'Default message');
    
    let callback = (val, oldVal, uri) => {
      this.msg = this.$ls.get('sync_msg')
    } 
    
    this.$ls.on('sync_msg', callback)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  background-color: bisque;
}
</style>
