<template>
  <div>
    <h1>CBC</h1>
    <p>字串:</p><input type="text" v-model="text" style="width:60%;" placeholder="請輸入字串">
    <p>金鑰:</p><input type="text" v-model="kkey" style="width:60%;" placeholder="請輸入key16位元">
    <p>初始向量:</p><input type="text" v-model="iiv" style="width:60%;" placeholder="請輸入初始向量16位元">
    <button @click="key1()">加密</button>
    <button @click="key2()">解密</button>
    <div>加密:{{aes}}</div>
    <div>解密:{{decode}}</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      text:"",
      kkey:"",
      iiv:"",
      decode:"",
      aes:""
    }
  },
  methods:{
    key1(){
      var CryptoJS = require("crypto-js");
      var key = CryptoJS.enc.Utf8.parse(this.kkey);
      var iv = CryptoJS.enc.Utf8.parse(this.iiv);  
      var plaintText = this.text; 
      var encrypted = CryptoJS.AES.encrypt(plaintText, key, {
        iv: iv,
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7
    });;
      console.log("加密後："+encrypted);
      this.aes = encrypted.toString();
    },
    key2(){
      var CryptoJS = require("crypto-js");
      var key = CryptoJS.enc.Utf8.parse(this.kkey);
      var iv = CryptoJS.enc.Utf8.parse(this.iiv);  
      var decrypted = CryptoJS.AES.decrypt(this.aes, key, {
        iv: iv,
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7
    });
    decrypted = CryptoJS.enc.Utf8.stringify(decrypted);
    console.log("解密後:"+decrypted)
      this.decode = decrypted;
    }
  }
  
}
</script>

<style>

</style>
