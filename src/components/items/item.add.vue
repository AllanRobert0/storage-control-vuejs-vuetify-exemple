<template>
  <v-container>
       <v-dialog
        v-model="showDialog"
        persistent
        max-width="600px"
      >
        <v-card>
          <v-card-title>
            <span class="headline">Adicionar Item</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>

                <v-btn
                  block
                  color="blue-grey"
                  class="ma-2 white--text"
                  @click="ativarScanner()"
                >
                  Scanear Codigo
                  <v-icon
                    right
                    dark
                    size="35"
                  >
                    mdi-barcode
                  </v-icon>
                </v-btn>
                
                <v-col
                  cols="12"
                  sm="6"
                  md="4"
                >
                  <v-text-field
                    label="Código de Barras *"
                    v-model="newItem.barcode"
                    required
                  ></v-text-field>
                </v-col>

                <v-col
                  cols="12"
                  sm="6"
                  md="4"
                >
                  <v-text-field
                    label="Nome do Item *"
                    v-model="newItem.name"
                    required
                  ></v-text-field>
                </v-col>

                <v-col
                  cols="12"
                  sm="6"
                  md="4"
                >
                  <v-text-field
                    label="Preço do Item *"
                    v-model="newItem.price"
                    required
                    type="number"
                  ></v-text-field>
                </v-col>
                

              </v-row>
            </v-container>
            <!-- <small>*Prrencha todos os Campos</small> -->
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="blue darken-1"
              text
              @click="onCancel()"
            >
              Cancelar
            </v-btn>
            <v-btn
              color="blue darken-1"
              text
              @click="onSave()"
            >
              Salvar
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <Scanner
        :showScanner="openScanner"
        v-on:onSuccessScan="fillBarcodeField"
        v-on:onFailedScan="closeScanDialog"
      />
<!-- 
         -->
  </v-container>
</template>

<script>
  import Scanner from '../../misc/scanner';

  export default {
    name: 'ItemAdd',
    components: {
      Scanner,
    },
    props: {
        showDialog: Boolean
    },
    data: () => ({
      newItem: {
        name: "",
        price: "",
        barcode: "",
      },
      openScanner: false,
    }),
    methods: {
      onSave(){
        if(!this.validateForm()) return;
        let newItemParam = {...this.newItem};
        this.$emit("onSaveItem", newItemParam);
        this.cleanFormFields();
      },
      onCancel(){
        this.$emit("onCancelAddItem");
        this.cleanFormFields();
      },
      cleanFormFields(){
        this.newItem.name = "";
        this.newItem.price = "";
        this.newItem.barcode = "";
      },
      validateForm(){
        if(
          this.newItem.name === ""
          || this.newItem.price === ""
          || this.newItem.barcode === ""
          ) return false;

        return true;
      },
      ativarScanner(){
        this.openScanner = true;
        console.log("Ativando o scanner -> ", this.openScanner);
      },
      fillBarcodeField(decodedCode){
        this.newItem.barcode = decodedCode;
        this.openScanner = false;
      },
      closeScanDialog(){
        this.openScanner = false;
      }
    }
  }
</script>