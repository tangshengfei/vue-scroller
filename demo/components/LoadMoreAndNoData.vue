<template>
  <div>
    <nav-bar title="Load More & No Data"></nav-bar>
    <scroller :on-infinite="infinite" ref="my_scroller">
      <div style="height: 44px;"></div>
      <div v-for="(item, index) in items"
          class="row" :class="{'grey-bg': index % 2 == 0}">
        {{ item }}
      </div>
    </scroller>
  </div>
</template>
<script>
  import Scroller from 'vue-scroller'
  import NavBar from './NavBar.vue'

  export default {
    components: {
      Scroller,
      NavBar
    },

    data () {
      return {
        items: []
      }
    },

    mounted() {
      for (let i = 1; i <= 20; i++) {
        this.items.push(i + ' - keep walking, be 2 with you.')
      }
      this.top = 1
      this.bottom = 20
      setTimeout(() => {
        this.$refs.my_scroller.resize()
      })
    },

    methods: {
      infinite() {
        if (this.bottom >= 30) {
          setTimeout(() => {
            this.$refs.my_scroller.finishInfinite(true)
          }, 1500)
          return;
        }

        setTimeout(() => {
          let start = this.bottom + 1
          for (let i = start; i < start + 10; i++) {
            this.items.push(i + ' - keep walking, be 2 with you.')
          }
          this.bottom = this.bottom + 10;
          setTimeout(() => {
            this.$refs.my_scroller.finishInfinite()
          })
        }, 1500)
      }
    }
  }
</script>


