<template>
<div id="app">
  <GameHeader :my-color= 'myColor'/>
    <Buttons :my-color='myColor' :colors='colors' :message='message'/>
    <Item v-for="(color, index) in colors" :color='color' :index="index" :key="myKey(color)"
        :colors='colors' :get-ganador="getGanador"/>
</div>
  
</template>

<script>
import GameHeader from './components/GameHeader.vue';
import Buttons from './components/Buttons.vue';
import Item from './components/Item.vue';

export default {
  name: 'app',
  components: {
    GameHeader,
    Buttons,
    Item
  },
    data() {
      return{
        myColor: {
                  r: 0,
                  g: 0,
                  b: 0
              },
              colors: [],
              message:"",
              colorclickeado:"",
              }
    },
    mounted() {
     
    },
    methods: {
        getGanador(colorcuadrado, cuadradoIndex){
            if(JSON.stringify(colorcuadrado) === JSON.stringify(this.myColor)){
                this.message="Ganaste";
                for (let index = 0; index < this.colors.length; index++) {
                    Object.assign(this.colors[index], colorcuadrado);
                  }
            }else{
                this.message="Intenta de nuevo";
                this.colors[cuadradoIndex].r = 35;
                this.colors[cuadradoIndex].g = 35;
                this.colors[cuadradoIndex].b = 35;
            }
        },
        myKey(color){
            const randomNumber = Math.random() * 100000;
            return '' + randomNumber + color.r +color.g +color.b;
        }
    },
    computed: {}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
	background: #232323;
	margin: 0;
	font-family: "Montserrat", "Avenir";
}

h1 {
	font-weight: normal;
	line-height: 1.1;
	padding: 20px 0;

}
#navigator {

	background: #ffffff;
	height: 30px;
	text-align: center;
	margin: 0;
	margin-top: -30px;

}
#header {
	transition: all 0.3s;
	background: steelblue;
	text-transform: uppercase;
	text-align: center;
	margin: 0;
	color: white;
	
}
#color_display {
	font-size: 200%;
}


.square {
	width: 30%;
	background: blue;
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;

}
#container {
	margin: 20px auto;
	max-width: 600px;
}
#message {
	color: #0a0404;
	display: inline-block;
	width: 20%;
}
.selected {
	background-color: steelblue;
	color: white;
}
button {
	border: none;
	background-color: white;
	font-family: "Montserrat", "Avenir";
	text-transform: uppercase;
	height: 100%;
	font-weight: 700;
	letter-spacing: 1px;
	color: steelblue;
	transition: all 0.3s;
	outline: none;
}
button:hover {
	color: white;
	background-color: steelblue;
}
</style>
