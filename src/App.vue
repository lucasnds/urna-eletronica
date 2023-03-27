<template>
  <div class="container">

    <div class="container__results">
      <div class="container__results__header">
        <h4>SEU VOTO PARA</h4>
        <h5 align="center">MELHOR CANTOR(A) DA BAHIA</h5>
        <br>
      </div>
      <div class="container__results__result">
        <div class="view" >
          <div class="view__screen" v-for="(value, index) in numberVoto.padEnd(2,' ')" :key="index">{{value}}</div>
        </div>
        <br>
        <div class="container__results__main" v-for="(cantor, index) in this.cantores" :key="index">
            <div v-if="numberVoto == cantor.number">
              <p>Nome:{{cantor.name}}</p>
              <p>Gênero musical:{{cantor.style}}</p>
            </div>
            <img v-if="numberVoto == cantor.number" :src="cantor.photo" alt="foto do cantor(a)">
        </div>
        
      </div>
      <div class="container__results__footer">
        <hr>
        <p>Aperte a tecla:</p>
        <p>CONFIRMAR para CONFIRMAR seu voto</p>
        <p>CORRIGIR para RESETAR os números discados</p>
        <p>BRANCO para anular seu voto</p>
      </div>
    </div>

    <div class="container__disk">

      <div class="container__disk__buttons">
        <button class="container__disk__button" @click="addNumber(1)"> <span>1</span></button>
        <button class="container__disk__button" @click="addNumber(2)"> <span>2</span></button>
        <button class="container__disk__button" @click="addNumber(3)"> <span>3</span></button>
        <button class="container__disk__button" @click="addNumber(4)"> <span>4</span></button>
        <button class="container__disk__button" @click="addNumber(5)"> <span>5</span></button>
        <button class="container__disk__button" @click="addNumber(6)"> <span>6</span></button>
        <button class="container__disk__button" @click="addNumber(7)"> <span>7</span></button>
        <button class="container__disk__button" @click="addNumber(8)"> <span>8</span></button>
        <button class="container__disk__button" @click="addNumber(9)"> <span>9</span></button>
        <div></div>
        <button class="container__disk__button" @click="addNumber(0)"> <span>0</span></button>
        <div></div>
        <button class="operations" id="white" @click="whiteButton()">BRANCO</button>
        <button class="operations" id="correct" @click="resetNumber()">CORRIGIR</button>
        <button class="operations" id="confirm" @click="confirmButton()">CONFIRMAR</button>
      </div>
    </div>
  </div>
</template>

<script>
import confirmAudio from '@/assets/Audio/confirm.wav'

export default {
  name: 'App',
  data(){
  return{
    numberVoto:'',
      cantores: [{
                      photo: "https://api.varelanet.com.br/fotos/varela_noticias/24724/FOTO_NOTICIA_2.jpg?v=dd548414fc8cf13ca07291c0adc1e584",
                      name: "O polêmico",
                      style: "Pagode baiano",
                      number: 23
                  },
                  {
                    photo: "https://www.cnnbrasil.com.br/wp-content/uploads/sites/12/2023/02/Snapinsta.app_1080_325711923_612665274004261_7509449942068813119_n-e1675893242515.jpg",
                      name: "Léo Santana",
                      style: "Pagode baiano",
                      number: 30
                  },
                  {
                    photo: "https://www.ivetesangalo.com/wp-content/themes/ivete-sangalo/components/index/2022/ivete-topo.png",
                      name: "Ivete Sangalo",
                      style: "MPB",
                      number: 14
                  },
                  {
                    photo: "https://www.bahianoiteedia.com.br/wp-content/uploads/2022/03/edson-gomes.jpg",
                      name: "Edson Gomes",
                      style: "Reggae",
                      number: 42
                  }
                  ,{
                    photo: "data:image/png;base64,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",
                      name: "Voto nulo",
                      style: "Voto nulo",                                                                                                                                                   
                      number:'00'                                                
                  },
                  {
                    photo: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEX///+nxBvIAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC",
                      name: "Voto branco",
                      style: "Voto branco",
                      number: '  '
                  }]
              
            }
          },
          methods:{
            addNumber(number){
              if(this.numberVoto.length == 2){
                return false
              }
              this.numberVoto += '' + number
            },
            resetNumber(){
              this.numberVoto = ''
            },
            whiteButton(){
              this.numberVoto = '  '
            },
            confirmButton(){
              if(this.numberVoto != ''){
                var audio = new Audio(confirmAudio)
                audio.play()
              }
              this.resetNumber()
            }

          
          }
}

</script >
<style lang="scss">
@import "@/assets/SASS/main.scss";
</style>
