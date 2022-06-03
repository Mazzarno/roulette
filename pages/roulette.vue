<template>
  <vs-row justify="center" align="center" class="home">
    <vs-col w="12">
      <FortuneWheel
        style="width: 600px"
        :canvas="canvasOptions"
        :prizes="prizes"
        :verify="cavansVerify"
        @rotateStart="onCanvasRotateStart"
        @rotateEnd="onRotateEnd"
      />
      <vs-dialog v-if="kdo" width="750px" not-padding blur v-model="kdopopup">
        <template #header>
          <h4>
            <h1>Vous avez gagné {{ kdo }}</h1>
          </h4>
        </template>

        <div class="con-content">
          <img width="700px" :src="require(`@/assets/img/${kdoimg}`)" alt="" />
        </div>

        <template #footer>
          <div class="con-footer">
            <vs-button @click="kdopopup = false" transparent> Ok </vs-button>
          </div>
        </template>
      </vs-dialog>
    </vs-col>
  </vs-row>
</template>
<script>
import FortuneWheel from 'vue-fortune-wheel'
import 'vue-fortune-wheel/lib/vue-fortune-wheel.css'
export default {
  components: {
    FortuneWheel,
  },
  data() {
    return {
      kdopopup: false,
      kdo: '',
      kdoimg: '',
      cavansVerify: false, // Whether the turntable in canvas mode is enabled for verification
      canvasOptions: {
        borderWidth: 3,
        borderColor: '#EC9B3B',
        fontSize: '26',
        textLength: '20',
      },
      prizes: [
        {
          id: 1, //* The unique id of each prize, an integer greater than 0
          name: 'Jeu de cartes ', // Prize name, display value when type is canvas (this parameter is not needed when type is image)
          value: 'un jeu de cartes ', //* Prize value, return value after spinning
          img: 'jeudecartes.png',
          bgColor: '#293462', // Background color (no need for this parameter when type is image)
          color: '#ffffff', // Font color (this parameter is not required when type is image)
          probability: 55, //* Probability, up to 4 decimal places (the sum of the probabilities of all prizes
          weight: 1, // Weight, if useWeight is true, the probability is calculated by weight (weight must be an integer), so probability is invalid
        },
        {
          id: 2,
          name: "Pochette d'ordinateur ",
          value: "une pochette d'ordinateur",
          img: 'pochettelogo.png',
          bgColor: '#F24C4C',
          color: '#ffffff',
          probability: 20,
          weight: 1,
        },
        {
          id: 3,
          name: 'Batterie externe',
          value: 'une batterie externe',
          img: 'powerbanks_resize.jpg',
          bgColor: '#293462',
          color: '#ffffff',
          probability: 20,
          weight: 1,
        },
        {
          id: 4,
          name: 'Lot premium',
          value: 'un lot premium',
          img: 'win.png',
          bgColor: '#EC9B3B',
          color: '#ffffff',
          probability: 5,
          weight: 1,
        },
      ],
    }
  },
  methods: {
    onCanvasRotateStart(rotate) {
      this.$data.kdo = ''
      this.$data.kdoimg = ''
      if (this.canvasVerify) {
        const verified = true // true: the test passed the verification, false: the test failed the verification
        this.DoServiceVerify(verified, 2000).then((verifiedRes) => {
          if (verifiedRes) {
            console.log('Verification passed, start to rotate')
            rotate() // Call the callback, start spinning
            this.canvasVerify = false // Turn off verification mode
          } else {
            alert('Failed verification')
          }
        })
        return
      }
      console.log('onCanvasRotateStart')
    },
    onRotateEnd(prize) {
      this.$data.kdopopup = true
      this.$data.kdo = prize.value
      this.$data.kdoimg = prize.img
    },
    // Simulate the request back-end interface, verified: whether to pass the verification, duration: delay time
    DoServiceVerify(verified, duration) {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(verified)
        }, duration)
      })
    },
  },
}
</script>