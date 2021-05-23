<template>
  <v-container>
        <v-dialog
            v-model="showScanner"
            persistent
            max-width="600px"
        >
            <div >
                <StreamBarcodeReader
                @decode="(a, b, c) => onDecode(a, b, c)"
                @loaded="() => onLoaded()"
                ></StreamBarcodeReader>
            </div>

            <v-btn
                block
                color="red"
                class=" white--text"
                @click="onCancelScan()"
            >
                Canclar Scanamento
                
            </v-btn>
        </v-dialog>
  </v-container>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";

export default {
  name: "Scanner",
  props: {
    showScanner: Boolean,
    msg: String,
  },
  components: {
    StreamBarcodeReader,
  },
  data() {
    return {
        
    };
  },
  methods: {
    // eslint-disable-next-line no-unused-vars
    onDecode(a, b, c) {
        this.$emit("onSuccessScan", a);
    },
    onCancelScan(){
        this.$emit("onFailedScan");
    },
    onLoaded() {
      console.log("load");
    },
  },
};
</script>
<style scoped>
</style>
