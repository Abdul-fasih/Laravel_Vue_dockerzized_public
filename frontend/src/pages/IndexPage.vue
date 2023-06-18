<template>
  <q-page class="flex flex-center">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >
    <div>{{ text }}</div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data () {
    return {
      text: ''
  }},
  methods: {
    getMethod() {
      this.text = ''
      return new Promise((resolve, reject) => {
        this.$api.get('/test')
            .then((response) => {
              this.text = response.data
              resolve(response)
            })
            .catch((error) => {
              this.text = ''
              reject(error)
            })
      })
    }
  },
  created () {
    this.getMethod()
  }
})
</script>
