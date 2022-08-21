<template>
  <v-container class="">
    <v-toolbar>
      <v-toolbar-title> Guía de Discusión</v-toolbar-title>

      <v-spacer></v-spacer>

      <!-- <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn v-bind="attrs" v-on="on" text color="primary"> Import </v-btn>
        </template>
        <span>Importar Preguntas</span>
      </v-tooltip> -->
    </v-toolbar>
    <v-row no-gutters>
      <v-col cols="12" sm="6" md="8">
        <v-card class="mx-auto">
          <v-card-text>
            <div class="text-h5 black--text darken-3">Incorporar Encuesta</div>
          </v-card-text>
          <v-row no-gutters>
            <v-col cols="12" sm="4" md="12">
              <v-card class="pa-2" outlined v-if="!encuestaSelecionada">
                <v-btn
                  class="ma-1"
                  color="success"
                  x-small
                  plain
                  @click="dialogEncuesta = !dialogEncuesta"
                >
                  <v-icon>mdi-plus-circle</v-icon>
                  Add Items
                </v-btn>
              </v-card>
              <v-row no-gutters v-if="encuestaSelecionada">
                <v-col>
                  <v-card class="pa-2" outlined tile>
                    {{ datosEncuestaSelecionada.id }}
                  </v-card>
                </v-col>
                <v-col>
                  <v-card class="pa-2" outlined tile>
                    {{ datosEncuestaSelecionada.name }}
                  </v-card>
                </v-col>
                <v-col>
                  <v-card class="pa-2" outlined tile>
                    <v-btn
                      color="error"
                      x-small
                      plain
                      @click="removerEncuesta()"
                    >
                      Remover
                      <v-icon>mdi-delete</v-icon>
                    </v-btn>
                  </v-card>
                </v-col>
              </v-row>
              <v-dialog v-model="dialogEncuesta" persistent max-width="500px">
                <v-card color="">
                  <v-toolbar dense>
                    <v-spacer></v-spacer>

                    <v-icon
                      color="error"
                      x-large
                      @click="dialogEncuesta = !dialogEncuesta"
                      >mdi-close-circle</v-icon
                    >
                  </v-toolbar>
                  <v-card-title class="bg-ligth">
                    Encuestas
                    <v-spacer></v-spacer>
                    <v-text-field
                      v-model="search"
                      append-icon="mdi-magnify"
                      label="Search"
                      single-line
                      hide-details
                    ></v-text-field>
                  </v-card-title>
                  <v-data-table
                    :headers="headers"
                    :items="desserts"
                    :search="search"
                    :items-per-page="[5]"
                    :footer-props="{
                      'items-per-page-options': [5, 6, 7],
                      prevIcon: 'mdi-arrow-left-bold-circle-outline',
                      nextIcon: 'mdi-arrow-right-bold-circle-outline',
                      'items-per-page-text': 'Encuestas por Pagina',
                    }"
                  >
                    <template v-slot:item.actions="{ item }">
                      <v-tooltip bottom>
                        <template v-slot:activator="{ on, attrs }"
                          ><v-icon
                            v-bind="attrs"
                            v-on="on"
                            color="success"
                            @click="selectEncuesta(item)"
                          >
                            mdi-play-circle
                          </v-icon>
                        </template>
                        <span>Seleccionar Encuesta</span>
                      </v-tooltip>
                    </template>
                  </v-data-table>
                </v-card>
              </v-dialog>
            </v-col>
          </v-row>
        </v-card>
        <v-card class="mx-auto">
          <v-card-text>
            <div class="text-h5 black--text darken-3">
              Incorporar Preguntas a la conversación
            </div>
          </v-card-text>
          <v-row no-gutters>
            <v-col cols="12" sm="4" md="12">
              <v-card class="pa-2" outlined>
                <v-btn class="ma-1" color="success" x-small plain>
                  <v-icon>mdi-plus-circle</v-icon>
                  Add Items
                </v-btn>
              </v-card>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="4">
        <v-card class="overflow-hidden">
          <v-card class="d-flex justify-center mb-6" flat tile
            ><h2 class="font-weight-light">Datos Basicos</h2></v-card
          >
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    dialogEncuesta: false,
    search: "",
    headers: [
      {
        text: "Encuestas",
        align: "start",
        sortable: false,
        value: "name",
      },

      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [
      {
        id: 1,
        name: "Frozen Yogurt",
      },
      {
        id: 2,
        name: "Ice cream sandwich",
      },
      {
        id: 3,
        name: "Eclair",
      },
      {
        id: 4,
        name: "Cupcake",
      },
      {
        id: 5,
        name: "Gingerbread",
      },
      {
        id: 6,
        name: "Jelly bean",
      },
      {
        id: 7,
        name: "Lollipop",
      },
      {
        id: 8,
        name: "Honeycomb",
      },
    ],
    encuestaSelecionada: false,
    datosEncuestaSelecionada: "",
  }),
  methods: {
    selectEncuesta(item) {
      console.log(item);
      alert("selecionado" + item.id);
      this.datosEncuestaSelecionada = item;
      this.encuestaSelecionada = true;
      this.dialogEncuesta = false;
    },
    removerEncuesta() {
      this.encuestaSelecionada = false;
      this.datosEncuestaSelecionada = "";
    },
  },
};
</script>