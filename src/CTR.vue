<template>
  <div>
    <h1>CTR</h1>
    <p>字串:</p><input type="text" v-model="text" style="width:60%;" placeholder="請輸入字串">
    <button @click="key2()">加密</button>
    <button @click="key3()">解密</button>
    <div>加密:{{aes}}</div>
    <div>解密:{{decode}}</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      text:"",
      aes:"",
      decode:"",
    }
  },
  
  methods:{
    key2(){
      var aesjs = require('aes-js');
      var key = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 ];
      var textBytes = aesjs.utils.utf8.toBytes(this.text);
      var aesCtr = new aesjs.ModeOfOperation.ctr(key);
      var encryptedBytes = aesCtr.encrypt(textBytes);
      var encryptedHex = aesjs.utils.hex.fromBytes(encryptedBytes);
      console.log(encryptedHex);
      this.aes = encryptedHex;
    },
    key3(){
      var aesjs = require('aes-js');
      var key = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 ];
      var encryptedBytes = aesjs.utils.hex.toBytes(this.text);
      var aesCtr = new aesjs.ModeOfOperation.ctr(key);
      var decryptedBytes = aesCtr.decrypt(encryptedBytes);
      var decryptedText = aesjs.utils.utf8.fromBytes(decryptedBytes);
      console.log(decryptedText);
      this.decode = decryptedText;
    }
  }
  
}
</script>

<style>

</style>
