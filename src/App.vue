<template>
  <div id="app">
   <h1>{{meg}}</h1>
   <CBC></CBC>
   <ECB></ECB>
   <CFB></CFB>
   <OFB></OFB>
   <CTR></CTR>
  </div>
</template>

<script>
import CBC from './CBC.vue'
import ECB from './ECB.vue'
import CFB from './CFB.vue'
import OFB from './OFB.vue'
import CTR from './CTR.vue'
export default {
  name: 'app',
  data(){
    return{
      meg:'個人報告 資工三乙 李宗緯 10411235'
    }
  },
  components:{
    CBC,
    ECB,
    CFB,
    OFB,
    CTR
  }
}
</script>

<style scoped>
h1{
  text-align:center;
  color: rebeccapurple;
}
</style>
