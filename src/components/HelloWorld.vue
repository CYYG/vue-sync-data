<template>
  <div class="hello">
    <h1>Une belle page Vue</h1>
    <h2>{{ msg }}</h2>
    <input v-model="msg" @input="storeOnLocal" placeholder="modifiez-moi">
    <section>
      <h3>Synchroniser les autres pages</h3>
      <input type="radio" v-model="sync" value="1">Oui
      <input type="radio" v-model="sync" value="0">Non
    </section>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: this.$ls.get('msg'),
      sync: "1"
    }
  },
  methods: {
    storeOnLocal() { 
      if(this.sync === "1") {
        this.$ls.set('msg', this.msg);
      }
    }
  },
  mounted() {
    this.$ls.set('msg', 'boo');
    
    let callback = (val, oldVal, uri) => {
      this.msg = this.$ls.get('msg')
    } 
    
    this.$ls.on('msg', callback)
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
