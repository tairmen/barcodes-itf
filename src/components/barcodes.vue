<template>
  <div class="hello">
    <h2>{{ digitPartTitle }}</h2>
    <input type="number" step="1" v-model="numberValue" /><br>
    <barcode :value="barcodeValue" format="ITF14">
      No valid
    </barcode>
    <h2>{{ textPartTitle }}</h2>
    <input type="text" maxlength="5" v-model="textValue" /><br>
    <barcode :value="barcode2Value" format="ITF14">
      No valid
    </barcode>
    <h3 v-if="errorMess">Only ascii symbols</h3>
  </div>
</template>
<script>
import VueBarcode from 'vue-barcode';
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      digitPartTitle: "Input digit from 0 to 10^14",
      textPartTitle: "Input text max 5 symbols",
      barcodeValue: '0000000000000',
      barcode2Value: '0000000000000',
      numberValue: '0',
      textValue: '',
      errorMess: false
    }
  },
  watch: {
    numberValue() {
      let val = parseInt(this.numberValue);
      if (val > 9999999999999 || val < 0) {
        this.barcodeValue = "a";
      } else {
        let newBarVal = "";
        let i = 0;
        for (i; i < this.numberValue.length; i++) {
          newBarVal += this.numberValue[i];
        }
        for (let j = i; j < 13; j++) {
          newBarVal = "0" + newBarVal;
        }
        this.barcodeValue = newBarVal;
      }
    },
    textValue() {
      if (this.textValue.length > 0) {
        if (this.textValue[this.textValue.length - 1].charCodeAt() > 127) {
          this.errorMess = true;
        } else {
          this.errorMess = false;
          let newBarVal = 0;
          for (let i = 0; i < this.textValue.length; i++) {
            newBarVal += this.textValue[i].charCodeAt() * Math.pow(128, this.textValue.length - 1 - i);
          }
          newBarVal = newBarVal.toString();
          for (let j = newBarVal.length; j < 13; j++) {
            newBarVal = "0" + newBarVal;
          }
          this.barcode2Value = newBarVal;
        }
      }
    }
  },
  components: {
    'barcode': VueBarcode
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
