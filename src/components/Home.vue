<template>
  <Page class="page">
    <ActionBar class="action-bar" title="Home"/>

    <StackLayout>
      <Button class="btn btn-primary" @tap="$router.push('/counter')">Counter</Button>
      <Button class="btn btn-primary" @tap="$router.push('/hello')">Hello World</Button>
    </StackLayout>

  </Page>
</template>

<script>
import Vue from "nativescript-vue";
import Vuex from "vuex";

Vue.use(Vuex);
let vue = new Vue();

export default {
  name: "Home",
  data() {
    return {
    };
  },
  methods: {
  },
  mounted: function() {
      var bitcoinjs = require('bitcoinjs-lib');
      var bip32utils = require('bip32-utils');

      var seed = "05789456e714a0c45366637a9bd1ae0e2be885d0d026ef1f1da08c83e4b29412"
      const seedHex = seed.toString('hex')
      const hdNode = bitcoinjs.HDNode.fromSeedHex(seedHex)
      var chain = new bip32utils.Chain(hdNode)

      for (var k = 0; k < 1; k++) {
        chain.next()
      }

      var privateKey = chain.getAll().map((x) => chain.derive(x).keyPair.toWIF())
      console.log(privateKey)
  }
};
</script>
