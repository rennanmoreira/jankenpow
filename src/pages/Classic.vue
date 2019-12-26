<template>
  <div class="classic">
    <div class="scroll-area">
      <!-- <div :style="`top: ${scrollItemsTop}%;`" class="scroll-items">
        <div
          v-for="({type, color}, index) in items"
          :key="`item${index}`"
          :id="'item'+index"
          :class="`option-item dark img-${type} bg-${color} mv-10`">
        </div>
      </div> -->
      <!-- <div class="scroll-items"> -->
        <div
          v-for="({type, action}, index) in displayItems"
          :key="`item${index}`"
          :id="`item${index}`"
          :class="`option-item dark img-${type} bg-${action} mv-10`">
        </div>
      </div>
    <!-- </div> -->

    <div class="pontuation-area">
      <div class="d-flex jc-space-between">
        <span>pontuação = {{score}}</span>
        <span>restantes = {{items.length - timesTouched}}</span>
      </div>
    </div>

    <Operation @touch="touch($event)"/>

    <Logo class="mini-logo"/>

    <div :class="['initial-page', {'hide': isStarted}]" >
      <Logo class="logo"/>
      <span class='start-btn' @click="start">START</span>
    </div>
    
  </div>
  
</template>

<script>
import Operation from '@/components/Operation.vue'
import Logo from '@/components/Logo.vue'

export default {
  components: { Operation, Logo },
  data: () => ({
    items: [
      { type: 'stone', action: 'draw', result: undefined },
      { type: 'scissor', action: 'win', result: undefined },
      { type: 'stone', action: 'lose', result: undefined },
      { type: 'scissor', action: 'win', result: undefined },
      { type: 'paper', action: 'lose', result: undefined },
      { type: 'paper', action: 'win', result: undefined },
      { type: 'scissor', action: 'draw', result: undefined },
      { type: 'paper', action: 'win', result: undefined },
      { type: 'stone', action: 'lose', result: undefined },
      { type: 'stone', action: 'draw', result: undefined },
      { type: 'stone', action: 'draw', result: undefined },
      { type: 'scissor', action: 'win', result: undefined },
      { type: 'stone', action: 'lose', result: undefined },
      { type: 'scissor', action: 'win', result: undefined },
      { type: 'paper', action: 'lose', result: undefined },
      { type: 'paper', action: 'win', result: undefined },
      { type: 'scissor', action: 'draw', result: undefined },
      { type: 'paper', action: 'win', result: undefined },
      { type: 'stone', action: 'lose', result: undefined },
      { type: 'stone', action: 'draw', result: undefined },
    ],
    displayItems: [],
    timesTouched: 0,
    score: 0,
    isStarted: false
  }),
  methods: {
    delay: ms => new Promise(res => setTimeout(res, ms)),
    touch(event) {
      if (this.timesTouched === this.items.length) return
      
      this.items[this.timesTouched].result = this.isScored(event, this.items[this.timesTouched])
      this.timesTouched++;
    },
    isScored(event, item) {
      const rules = [
        { win: 'paper', lose: 'stone' },
        { win: 'stone', lose: 'scissor' },
        { win: 'scissor', lose: 'paper' },
      ]

      this.score++
      if (item.action === 'draw' && event === item.type) { return true }
      if (item.action === 'lose' && rules.some(i => item.type === i.lose && event === i.win)) { return true }
      if (item.action === 'win' && rules.some(i => item.type === i.win && event === i.lose)) { return true }

      this.score--
      return false
    },
    async start() {
      this.isStarted = true

      this.timesTouched = 0
      this.displayItems = []
      for(let i = 0; i < this.items.length; i++){
        await this.delay(1500)
        this.displayItems.push(this.items[i])
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .classic {
    height: 100%;
    background-color: #FCFCFC;

    .mini-logo {
      position: absolute;
      left: 5px;
      bottom: 5px;
      z-index: 1;
    }

    .logo {
      font-size: 40px;
    }

    .initial-page {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
      background: #1D1D1D;
      z-index: 1;
      flex-direction: column;

      &.hide {
        top: 100%;
        animation: slide 0.5s linear;
      }

      .start-btn{
        text-align: center;
        margin:15px;
        font-weight: bold;
        padding: 10px 10px 10px 10px ;
        background-color: lightgray;
        text-shadow: -1px -1px black, 1px 1px white;
        color: gray;
        -webkit-border-radius: 7px;
        -moz-border-radius: 7px;
        -o-border-radius: 7px;
        border-radius: 7px;
        box-shadow: 0 .2em gray; 
        cursor: pointer;
        width: 110px;
      }
    }

    .scroll-area {
      top: -100px;
      width: 100%;
      height: calc(100% - 150px);
      position: absolute;
      display: flex;
      justify-content: center;
        // align-items: center;
        // flex-direction: column;

      // .scroll-items {
      //   top: -100px;
      //   width: 100%;
      //   // height: 100%;
      //   // position: fixed;
      //   transition: top 10s linear;
      //   display: flex;
      //   align-items: center;
      //   justify-content: center;
      //   flex-direction: column;
      // }

      .option-item {
        // top: 0%;
        width: 100%;
        position: absolute;
        animation: slide 8s linear;
      }

      @keyframes slide {
        0% {
          top: 0%;
        }

        100% {
          top: 100%
        }
      }
    }

    .pontuation-area {
      color: #1D1D1D;
      padding: 10px 20px;
      position: absolute;
      width: -webkit-fill-available;
    }
  }
</style>
