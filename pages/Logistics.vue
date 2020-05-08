<template>
  <div class="order-wrapper">
    <v-card-title class="search-input">
      <v-text-field v-model="search" append-icon="mdi-magnify" label="検索" single-line hide-details></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="postpackagelist"
      sort-by="calories"
      class="elevation-1"
      show-select
      :search="search"
    >
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-toolbar-title>国際郵送業務</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="800px">
            <template v-slot:activator="{ on }">
              <v-btn color="primary" dark class="mb-2" v-on="on">新規</v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.name" label="Dessert name"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.calories" label="Calories"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.fat" label="Fat (g)"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.carbs" label="Carbs (g)"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
                <v-btn color="blue darken-1" text @click="save">Save</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
        <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: () => ({
    dialog: false,
    singleSelect: false,
    selected: [],
    loading: false,
    search: "",
    headers: [
      {
        text: "荷物番号",
        align: "start",
        sortable: false,
        value: "packageno",
        width:100
      },
      { text: "代理店", value: "carbs" },
      { text: "届け先", value: "calories" },
      { text: "依頼者", value: "fat" },
      { text: "外装サーズ", value: "size" },
      { text: "容積重量", value: "volweight" },
      { text: "実際重量", value: "realweight" },
      { text: "計上重量", value: "accweight" },
      { text: "単価", value: "unitprice" },
      { text: "貨物総価", value: "totalprice" },
      { text: "状態", value: "status" },
      { text: "操作", value: "actions", sortable: false }
    ],
    postpackagelist: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0
    },
    defaultItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0
    }
  }),
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "新規登録" : "Edit Item";
    }
  },
  watch: {
    dialog(val) {
      val || this.close();
    }
  },
  created() {
    this.initialize();
  },
  methods: {
    initialize() {
      this.loadlist();
    },
    editItem(item) {
      this.editedIndex = this.postpackagelist.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },
    deleteItem(item) {
      const index = this.postpackagelist.indexOf(item);
      confirm("Are you sure you want to delete this item?") &&
        this.postpackagelist.splice(index, 1);
    },
    close() {
      this.dialog = false;
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      }, 300);
    },
    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.postpackagelist[this.editedIndex], this.editedItem);
      } else {
        this.postpackagelist.push(this.editedItem);
      }
      this.close();
    },
    async loadlist() {
      this.loading=true;
      this.postpackagelist=[];
      axios
      .get("http://localhost:8080/api/orderlist")
      .then(response =>{
        this.postpackagelist = response.data;
      })
      .catch(error =>{
        alert(error);
      });
      this.loading=false;
    }
  }
};
</script>
<style scoped>
.search-input {
  padding-top: 0px;
}
</style>