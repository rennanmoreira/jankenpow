<template>
  <div class="classic">
    <div class="scroll-area">
      <div class="scroll-items">
        <div
          v-for="({type, color}, index) in items"
          :key="`item${index}`"
          :class="`option-item dark img-${type} bg-${color} mv-10`">
        </div>
      </div>
    </div>

    <div class="pontuation-area">
      <div class="d-flex jc-space-between">
        <span>pontuação = 0</span>
        <span>restantes = 0</span>
      </div>
    </div>

    <Operation/>

    <div class="mini-logo">
      <span class="font-red">J</span>
      <span class="font-yellow">a</span>
      <span class="font-blue">n</span>
      <span class="font-red">K</span>
      <span class="font-yellow">e</span>
      <span class="font-blue">n</span>
    </div>
  </div>
</template>

<script>
import Operation from '@/components/Operation.vue'

export default {
  components: { Operation },
  data: () => ({
    items: [
      { type: 'stone', color: 'yellow' },
      { type: 'scissor', color: 'blue' },
      { type: 'stone', color: 'red' },
      { type: 'scissor', color: 'blue' },
      { type: 'paper', color: 'red' },
      { type: 'paper', color: 'blue' },
      { type: 'scissor', color: 'yellow' },
      { type: 'paper', color: 'blue' },
      { type: 'stone', color: 'red' },
      { type: 'stone', color: 'yellow' },
      { type: 'stone', color: 'yellow' },
      { type: 'scissor', color: 'blue' },
      { type: 'stone', color: 'red' },
      { type: 'scissor', color: 'blue' },
      { type: 'paper', color: 'red' },
      { type: 'paper', color: 'blue' },
      { type: 'scissor', color: 'yellow' },
      { type: 'paper', color: 'blue' },
      { type: 'stone', color: 'red' },
      { type: 'stone', color: 'yellow' },
    ]
  })
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

    .scroll-area {
      top: 0;
      width: 100%;
      height: calc(100% - 250px);
      position: absolute;

      .scroll-items {
        top: 100%;
        width: 100%;
        height: 100%;
        position: absolute;
        transition: top 5s linear;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
      }
    }

    .pontuation-area {
      color: #1D1D1D;
      padding: 10px 20px;
      position: absolute;
      width: -webkit-fill-available;
    }

    .operation-area {
      width: 100%;
      height: 250px;
      bottom: 0px;
      position: absolute;
      background-color: #1D1D1D;
      box-shadow: 0px -2px 26px -13px rgba(0,0,0,0.75);
      -moz-box-shadow: 0px -2px 26px -13px rgba(0,0,0,0.75);
      -webkit-box-shadow: 0px -2px 26px -13px rgba(0,0,0,0.75);

      .controls {
        padding: 25px 0px;
        height: 200px;
        display: grid;
        justify-content: center;
        grid-template-columns: 100px 100px;
        grid-template-areas:
          "stone stone"
          "paper scissor";

        .label {
          font-size: 12px;
          margin: 2.5px 0px;
        }

        .stone {
          grid-area: stone;
          color: white;
          display: flex;
          align-items: center;
          flex-direction: column;
          justify-content: center;
        }

        .paper {
          grid-area: paper;
          color: white;
          display: flex;
          align-items: center;
          flex-direction: column;
          justify-content: center;
        }

        .scissor {
          grid-area: scissor;
          color: white;
          display: flex;
          align-items: center;
          flex-direction: column;
          justify-content: center;
        }
      }
    }
  }
</style>
