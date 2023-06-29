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
          v-for="({type, action, result}, index) in displayItems"
          :key="`item${index}`"
          :id="`item${index}`"
          :class="[`option-item dark img-${type} bg-${action} mv-10`, {'stopped': isStopped }]">
          <div v-if="result != undefined" class="option-item-result">
            <div class="option-item-result-background"></div>
            <div :class="`option-item-result-label result-${result}`">
              {{result ? "acertou" : "errou"}}
            </div>
          </div>
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

    <div class="mini-logo">
      <div :class="['start-btn', {'disabled': startedBlocked}]" @click="start">{{isStarted ? "RE-START" : "START"}}</div>
      <div class='stop-btn' @click="isStopped = !isStopped">STOP</div>
      <Logo />
    </div>
<!-- 
    <div :class="['initial-page', {'hide': isStarted}]" >
      <Logo class="logo"/>
      <span class='start-btn' @click="start">START</span>
    </div> -->
    
  </div>
  
</template>

<script>
import Operation from '@/components/Operation.vue'
import Logo from '@/components/Logo.vue'

let initializeItem = () => [
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
]

export default {
  components: { Operation, Logo },
  data: () => ({
    items: initializeItem(),
    displayItems: [],
    timesTouched: 0,
    score: 0,
    isStarted: false,
    startedBlocked: false,
    isStopped: false,
    timeout: setTimeout(() => {}, 1500)
  }),
  methods: {
    sleep(milliseconds) {
      return new Promise((resolve) => this.timeout(resolve, milliseconds));
    },
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
      if (this.startedBlocked) return

      this.items = initializeItem()
      this.timesTouched = 0
      this.displayItems = []
      this.score = 0
      this.isStarted = true
      this.startedBlocked = true
      const sleep = ms => new Promise(r => setTimeout(r, ms));
      let i = 0

      do {
        await sleep(1500)
        console.log('teste '+i)
        this.displayItems.push(this.items[i])
        i++
      } while (i < this.items.length)

      this.startedBlocked = false
    },
    stop(){

    }
  }
}
</script>

<style lang="scss" scoped>
  .classic {
    height: 100%;
    background-color: #FCFCFC;

    .start-btn, .stop-btn{
      text-align: center;
      margin:15px 2px;
      font-weight: bold;
      padding: 5px 0px;
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

      &.disabled {
        opacity: 0.4;
      }
    }

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
        border-radius: 50px;
        width: 100%;
        position: absolute;
        animation: slide 10s linear;

        .option-item-result {
          width: 100%;
          height: 100%;
          border-radius: 50px;
          position: absolute;
          display: flex;
          justify-content: center;
          align-items: center;

          .option-item-result-background {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50px;
            opacity: 0.7;
            background-color: black;
          }
          
          .option-item-result-label {
            position: absolute;
            display: flex;
            align-items: center;
            justify-content: center;

            opacity: 1;
            font-size: 18px;
          }
          .result-true {
            color: #23b926;
          }

          .result-false {
            color: #ee5f5b;
          }

        }


      }
      
      .stopped {
        animation-play-state: paused;
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


  // .blink {
  //   animation: blink-blinkingFrames 1s steps(5, start);
  //   -webkit-animation: blink-animation 1s steps(5, start);
  // }
  // @keyframes blink-animation {
  //   0% {opacity: 1.00;}
  //   50% {opacity: 0.00;}
  //   100% {opacity: 1.00;}
  // }
  // @-webkit-keyframes blink-animation {
  //   0% {opacity: 1.00;}
  //   50% {opacity: 0.00;}
  //   100% {opacity: 1.00;}
  // }
</style>
