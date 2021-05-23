<template>
  <v-container>
    <v-alert
    v-if="items.length === 0"
      color="green"
      border="left"
      elevation="2"
      colored-border
    >
      Adicione um Item tocando no botão <v-icon>mdi-plus-circle</v-icon>
    </v-alert>
    <v-col
      v-else
      v-for="(item, i) in items"
      :key="i"
      cols="12"
    >
      <v-card
        class="mx-auto"
        max-width="400"
      >
        <v-img
          class="white--text align-end"
          height="200px"
          src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
        >
          <!-- <v-card-title>Top 10 Australian beaches</v-card-title> -->
        </v-img>

        <!-- <v-card-subtitle class="pb-0">
          Item Número {{ i + 1 }} 
        </v-card-subtitle> -->

        <v-card-text class="text--primary">
          <div>{{ item.name }}</div>
          <h3> R$ {{ item.price }}</h3>
          <v-icon>mdi-barcode</v-icon>
          {{ item.barcode }}
        </v-card-text>

        <v-card-actions>
          <v-btn
            class="ml-2 mt-5"
            outlined
            rounded
            small
          >
            Vender
            <v-icon>mdi-currency-usd</v-icon>
          </v-btn>

          <v-btn
            class="ml-2 mt-5"
            outlined
            rounded
            small
          >
            Compartilhar
            <v-icon>mdi-whatsapp</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>

    <v-fab-transition>
      <v-btn
        @click="changeFloatingButton"
        :key="floatingIcon"
        :color="floatingColor"
        dark
        absolute
        bottom
        right
        fab
        fixed
        class="v-btn--floating"
      >
        <v-icon>{{ floatingIcon }}</v-icon>
      </v-btn>
    </v-fab-transition>
    
    <div >
      <ItemsAdd
        :showDialog="addNewItem"
        v-on:onSaveItem="saveItem"
        v-on:onCancelAddItem="changeFloatingButton"
      />
    </div>

  </v-container>
</template>

<script>
  import ItemsAdd from './item.add';

  export default {
    name: 'ItemList',

    components: {
      ItemsAdd,
    },

    data: () => ({
      floatingIcon: "mdi-plus",
      floatingColor: "green",
      addNewItem: false,
      items: [
        // {
        //   name: 'Erva Mate Menta',
        //   price: '25,00',
        //   barcode: '11223344',
        // },
        // {
        //   name: 'Erva Mate Abacaxi',
        //   price: '25,00',
        //   barcode: '11223344',
        // },
        // {
        //   name: 'Erva Terere Menta',
        //   price: '25,00',
        //   barcode: '11223344',
        // },
        // {
        //   name: 'Erva Terere Abacaxi',
        //   price: '25,00',
        //   barcode: '11223344',
        // },
      ],
    }),
    methods: {
      changeFloatingButton(){
        if(this.addNewItem) {
          this.floatingIcon = "mdi-plus";
          this.floatingColor = "green";
          // todo: hide modal
          this.addNewItem = !this.addNewItem;
        } else {
          this.floatingIcon = "mdi-cancel";
          this.floatingColor = "red";
          // todo: show modal
          this.addNewItem = !this.addNewItem;
        }        
      },
      saveItem(newItemParam){
        this.items.push(newItemParam);
        this.changeFloatingButton();
      }
    }
  }
</script>

<style scoped>
.v-btn--floating {
  /* top: 80%; */
  margin-bottom: 20%;
}
</style>