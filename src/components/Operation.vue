<template>
  <div class="operation-area">
    <div class="controls">
      <div class="stone" @click="$emit('touch', 'stone')">
        <span class="option-item img-stone"></span>
        <div class="label">Pedra</div>
      </div>
      <div class="paper" @click="$emit('touch', 'paper')">
        <span class="option-item img-paper"></span>
        <div class="label">Papel</div>
      </div>
      <div class="scissor" @click="$emit('touch', 'scissor')">
        <span class="option-item img-scissor"></span>
        <div class="label">Tesoura</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {}
</script>

<style lang="scss" scoped>
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
</style>
