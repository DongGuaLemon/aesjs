<template>
  <div>
    <h1>CFB segmentSize為8</h1>
    <p>字串:</p><input type="text" v-model="text" style="width:60%;" placeholder="請輸入長度為8的倍數">
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
      var iv = [ 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36 ];
      var textBytes = aesjs.utils.utf8.toBytes(this.text);
      var segmentSize = 8;
      var aesCfb = new aesjs.ModeOfOperation.cfb(key, iv, segmentSize);
      var encryptedBytes = aesCfb.encrypt(textBytes);
      var encryptedHex = aesjs.utils.hex.fromBytes(encryptedBytes);
      console.log(encryptedHex);
      this.aes = encryptedHex;
    },
    key3(){
      var aesjs = require('aes-js');
      var key = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 ];
      var iv = [ 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36 ];
      var segmentSize = 8;
      var encryptedBytes = aesjs.utils.hex.toBytes(this.text);
      var aesCfb = new aesjs.ModeOfOperation.cfb(key, iv, segmentSize);
      var decryptedBytes = aesCfb.decrypt(encryptedBytes);
      var decryptedText = aesjs.utils.utf8.fromBytes(decryptedBytes);
      console.log(decryptedText);
      this.decode = decryptedText;
    }
  }
  
}
</script>

<style>

</style>
