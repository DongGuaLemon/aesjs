<template>
  <div>
    <h1>ECB</h1>
    <p>字串:</p><input type="text" v-model="text" style="width:60%;" placeholder="請輸入字串">
    <p>金鑰:</p><input type="text" v-model="kkey" style="width:60%;" placeholder="請輸入key16位元">
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
      decode:"",
      aes:""
    }
  },
  methods:{
    key1(){
      var CryptoJS = require("crypto-js");
      var key = CryptoJS.enc.Utf8.parse(this.kkey);  
      var plaintText = this.text; // 明文  
      var encryptedData = CryptoJS.AES.encrypt(plaintText, key, {  
          mode: CryptoJS.mode.ECB,  
          padding: CryptoJS.pad.Pkcs7
        });
      console.log("加密前："+plaintText);
      console.log("加密後："+encryptedData);
      this.aes = encryptedData.toString();
      encryptedData = encryptedData.ciphertext.toString();  
      var encryptedHexStr = CryptoJS.enc.Hex.parse(encryptedData);  
      var encryptedBase64Str = CryptoJS.enc.Base64.stringify(encryptedHexStr);  
      var decryptedData = CryptoJS.AES.decrypt(encryptedBase64Str, key, {  
          mode: CryptoJS.mode.ECB,  
          padding: CryptoJS.pad.Pkcs7  
      });
      var decryptedStr = decryptedData.toString(CryptoJS.enc.Utf8);  
      console.log("解密後:"+decryptedStr);
          
    },
    key2(){
      var CryptoJS = require("crypto-js");
      var key = CryptoJS.enc.Utf8.parse(this.kkey);
      var pwd = this.text;  
      var decryptedData = CryptoJS.AES.decrypt(pwd, key, {  
         mode: CryptoJS.mode.ECB,  
        padding: CryptoJS.pad.Pkcs7  
      });
      var decryptedStr = decryptedData.toString(CryptoJS.enc.Utf8);
      console.log("解密後:"+decryptedStr)
      this.decode = decryptedStr;
    }
  }
  
}
</script>

<style>

</style>
