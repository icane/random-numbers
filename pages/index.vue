<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6" class="ma-3 pa-3">
      <v-card>
        <v-card-text>
          <v-form ref="form" lazy-validation @submit="generate">
            <v-row>
              <v-col class="pr-4">
                <v-text-field
                  v-model="dir_num"
                  type="number"
                  label="Número total de direcciones"
                  :rules="[numberRule]"
                ></v-text-field>
                <v-text-field
                  v-model="select_dir"
                  type="number"
                  label="Número de direcciones a seleccionar"
                  :rules="[numberRule]"
                ></v-text-field>
                <v-text-field
                  v-model="filename"
                  label="Nombre del fichero"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row align="center" justify="center">
              <v-btn class="ma-3 pa-3" color="primary" @click="generate"
                >Generar</v-btn
              >
            </v-row>
          </v-form>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import papaparse from 'papaparse'

export default {
  components: {},
  data() {
    return {
      dir_num: 10,
      dir_num_min: 0,
      select_dir: 5,
      selected_dirs: [],
      filename: 'sorteo_direcciones',
      numberRule: (v) => {
        if (!isNaN(parseInt(v)) && v >= 1) return true
        return 'El número debe ser mayor que 1'
      },
    }
  },
  methods: {
    generate() {
      this.dir_num = parseInt(this.dir_num)
      this.select_dir = parseInt(this.select_dir)
      this.selected_dirs = []
      const array = [...Array(this.dir_num + 1).keys()]
      array.shift() // array starts at 1
      console.log(array)

      for (let i = 0; i < this.select_dir; i++) {
        const random = Math.floor(Math.random() * array.length)
        this.selected_dirs.push({ number: array[random] })
        array.splice(random, 1)
      }
      console.log(this.selected_dirs)
      const csv = papaparse.unparse(this.selected_dirs, {
        delimiter: ';',
        encoding: 'ISO-8859-1',
        skipEmptyLines: true,
      })
      console.log(csv)
      this.download(this.filename + '.csv', csv)
    },
    getRandomInt(min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    download(filename, text) {
      if (window.navigator.msSaveBlob) {
        // IE y Edge
        const blob = new Blob([new Uint8Array([0xef, 0xbb, 0xbf]), text], {
          type: 'text/plain;charset=utf-8;',
        })
        window.navigator.msSaveBlob(blob, filename)
      } else {
        const element = document.createElement('a')
        element.setAttribute(
          'href',
          'data:text/plain;charset=utf-8,%EF%BB%BF' + encodeURIComponent(text)
        )
        element.setAttribute('download', filename)
        element.style.display = 'none'
        document.body.appendChild(element)
        element.click()
        document.body.removeChild(element)
      }
    },
  },
}
</script>
