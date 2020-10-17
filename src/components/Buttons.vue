<template>
  <div id="navigator">
            <button id="reset" @click="restart">New colors</button>
            <span id="message"> {{message}} </span>
            <button id="easy" :class="{ selected: !isHard }" @click="dificultadEasy">easy</button>
            <button id="hard" :class="{ selected: isHard }" @click="dificultadHard">hard</button>
    
        </div>
</template>

<script>
export default {
    data() {
		return {
            isHard:true,
            colorCount:6
        }
    },
  name: 'Buttons',
  props: ['myColor','colors', 'message'],
    created(){
        this.restart()
    },
    methods: {
        dificultadEasy(){
            if (this.isHard) {
                this.isHard = false;
                this.colorCount = 3;
                this.restart();
            }
        },
        dificultadHard(){
            if (!this.isHard) {
                this.isHard = true;
                this.colorCount = 6;
                this.restart();
            }
        },
        restart(){
            this.colors.splice(0, this.colors.length, ...this.createNewColors(this.colorCount));
            let pickedColor = this.colors[this.pickColor()];
            this.myColor.r = pickedColor.r;
            this.myColor.g = pickedColor.g;
            this.myColor.b = pickedColor.b;
        },
        createNewColors(numbers){
            let arr = [];
            for (var i = 0; i < numbers; i++) {
                arr.push(this.createRandomStringColor());
            }
            return arr;
        },
        createRandomStringColor(){
            return {
                r: this.randomInt(),
                g: this.randomInt(), 
                b: this.randomInt()
            };
        }, 
        randomInt(){
            return Math.floor(Math.random() * 256);
        },
        pickColor(){
            let quantity = 3;
            if (this.isHard) {
                quantity = 6;
            }
            return Math.floor(Math.random() * quantity );
        },        
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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