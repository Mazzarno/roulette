<template>
  <vs-row justify="center" align="center" class="home">
    <form @submit.prevent="validMDP">
      <div class="input-container">
        <input type="number" v-model="value1" class="number" min="0" max="9" />
        <h1 class="tiret">-</h1>
        <input type="number" v-model="value2" class="number" min="0" max="9" />
        <h1 class="tiret">-</h1>
        <input type="number" v-model="value3" class="number" min="0" max="9" />
        <h1 class="tiret">-</h1>
        <input type="number" v-model="value4" class="number" min="0" max="9" />
      </div>
      <vs-row justify="center" align="center">
        <vs-button size="xl" flat type="submit"> ENTRER </vs-button>
      </vs-row>
    </form>
  </vs-row>
</template>
<script>
export default {
  components: {},

  data() {
    return {
      value1: null,
      value2: null,
      value3: null,
      value4: null,
      totalValue: '',
    }
  },
  computed: {
    validMDP() {
      this.totalValue = this.value1 + this.value2 + this.value3 + this.value4
      if (this.$data.totalValue == 2514) {
        this.$router.push({ path: '/roulette' })
      } else {
        this.$router.push({ path: '/fail' })
      }
    },
  },
}
</script>
<style>
.number {
  width: 2em;
  text-align: center;
  border-radius: 15px;
  font-size: 20px;
}
.tiret {
  color: white;
  color: black;
  margin-left: 0.5em;
  margin-right: 0.5em;
}
.input-container {
  display: flex;

  padding: 1em;
  border-radius: 15px;
  
}
</style>