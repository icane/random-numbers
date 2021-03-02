<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app color="primary">
      <v-toolbar-title class="heading-primary" v-text="title" />
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer padless>
      <v-card width="100%" flat tile class="text-center">
        <v-card-text class="primary">
          <v-row no-gutters>
            <v-row align="center" justify="center">
              <a href="https://www.icane.es" target="blank">
                <v-img
                  alt="Logo ICANE"
                  src="logo/logo_icane.svg"
                  transition="scale-transition"
                  max-width="150"
                />
              </a>
            </v-row>
            <v-row align="center" justify="center">
              <a href="https://www.cantabria.es" target="blank">
                <v-img
                  alt="Logo Cantabria"
                  src="consejeria_hacienda/blanco_negro.svg"
                  transition="scale-transition"
                  max-width="150"
                />
              </a>
            </v-row>
            <v-row align="center" justify="center">
              <a href="https://www.caminolebaniego.com" target="blank">
                <v-img
                  alt="Logo Camino Lebaniego"
                  src="logo/camino_lebaniego_blanco.svg"
                  transition="scale-transition"
                  max-width="150"
                />
              </a>
            </v-row>
          </v-row>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Sorteo de direcciones',
    }
  },
}
</script>
<style scoped>
.heading-primary {
  color: #fff;
}
</style>
