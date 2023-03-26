<template>
  <div class="container">

    <div class="container__results">
      <p>Seu voto vai para</p>
    </div>

    <div class="container__disk">

      <div class="container__disk__buttons">
        <div class="container__disk__button"> <span>1</span></div>
        <div class="container__disk__button"> <span>2</span></div>
        <div class="container__disk__button"> <span>3</span></div>
        <div class="container__disk__button"> <span>4</span></div>
        <div class="container__disk__button"> <span>5</span></div>
        <div class="container__disk__button"> <span>6</span></div>
        <div class="container__disk__button"> <span>7</span></div>
        <div class="container__disk__button"> <span>8</span></div>
        <div class="container__disk__button"> <span>9</span></div>
        <div></div>
        <div class="container__disk__button"> <span>0</span></div>
        <div></div>
        <div class="operations" id="white">BRANCO</div>
        <div class="operations" id="correct">CORRIGIR</div>
        <div class="operations" id="confirm">CONFIRMAR</div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App'
  
}
</script >
<style lang="scss">
@import "@/assets/SASS/main.scss";
</style>
