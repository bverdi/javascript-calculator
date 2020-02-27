<template>
  <div id="app">
    <div id="calculator">
        <div class="result-operation" id="operation">
        <span id="text-result"></span>
        </div>
        <div class="result-operation" id="result">
        <span id="text-result">{{mynumber}}</span>
        </div>
        <div class="buttons">
          <b-row>
            <b-col cols="6" id="ac" class="internal-buttons" v-on:click="generator('AC')">
              <span id="text-ac">AC</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('/')">
              <span id="text-ac">/</span>
            </b-col>
            <b-col cols="3" id="multiple" class="internal-buttons" v-on:click="generator('*')">
              <span id="text-ac">*</span>
            </b-col>
          </b-row>
          <b-row>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('7')">
              <span id="text-ac">7</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('8')">
              <span id="text-ac">8</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('9')">
              <span id="text-ac">9</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('-')">
              <span id="text-ac">-</span>
            </b-col>
          </b-row>
          <b-row>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('4')">
              <span id="text-ac">4</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('5')">
              <span id="text-ac">5</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('6')">
              <span id="text-ac">6</span>
            </b-col>
            <b-col cols="3" id="dividing" class="internal-buttons" v-on:click="generator('+')">
              <span id="text-ac">+</span>
            </b-col>
          </b-row>
          <b-row id="row-special">
            <b-col cols="9" class="internal-buttons">
                <b-row>
                  <b-col cols="4" id="dividing" class="internal-buttons" v-on:click="generator('1')">
                    <span id="text-ac">1</span>
                  </b-col>
                  <b-col cols="4" id="dividing" class="internal-buttons" v-on:click="generator('2')">
                    <span id="text-ac">2</span>
                  </b-col>
                  <b-col cols="4" id="dividing" class="internal-buttons" v-on:click="generator('3')">
                    <span id="text-ac">3</span>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col cols="8" id="dividing" class="internal-buttons" v-on:click="generator('0')">
                    <span id="text-ac">0</span>
                  </b-col>
                  <b-col cols="4" id="dividing" class="internal-buttons" v-on:click="generator('.')">
                    <span id="text-ac">.</span>
                  </b-col>
                </b-row>
            </b-col>
            <b-col cols="3" id="equal" class="internal-buttons" v-on:click="generator('=')">
            <span id="text-ac">=</span>
            </b-col>
          </b-row>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data: function() {
    return {
      mynumber: [],
      myoperation: [],
      lastoperation: []
    }
  },
   methods: {
      generator: function(value)
      { 

        if(value == 'AC'){
          this.mynumber = [];
          this.mynumber = this.mynumber.length;
        }
        else if (value == '/' || value == '+' || value == '*' || value == '-')
        {
          if(this.myoperation.length <= 2){
            this.myoperation.push(this.mynumber);
            this.mynumber = value;
            this.lastoperation = value;
          }
          else {
            if(this.lastoperation == '/'){
              this.mynumber = parseFloat(parseFloat(this.myoperation[0])) / parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
            else if (this.lastoperation == '+') {
              this.mynumber = parseFloat(this.myoperation[0]) + parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
            else if (this.lastoperation == '*') {
              this.mynumber = parseFloat(this.myoperation[0]) * parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
            else if (this.lastoperation == '-'){
              this.mynumber = parseFloat(this.myoperation[0]) - parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
          }
        }
        else if (value == '='){
            this.myoperation.push(this.mynumber);
            if(this.lastoperation == '/'){
              this.mynumber = parseFloat(this.myoperation[0]) / parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
            else if (this.lastoperation == '+') {
              this.mynumber = parseFloat(this.myoperation[0]) + parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
            else if (this.lastoperation == '*') {
              this.mynumber = parseFloat(this.myoperation[0]) * parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
            else if (this.lastoperation == '-'){
              this.mynumber = parseFloat(this.myoperation[0]) - parseFloat(this.myoperation[1]);
              this.myoperation = [];
            }
        }
        else {
          if(this.mynumber != 0 && this.mynumber != '/' && this.mynumber != '+' && this.mynumber != '*' && this.mynumber && '-'){
            this.mynumber = this.mynumber.concat(value);
          }
          else {
          this.mynumber = value;
          }
        }
      }
   }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: lightblue;
}

#calculator {
  margin: 50px auto 50px auto;
  width: 30%;
  border-top: 2px solid gray;
  border-bottom: 2px solid gray;
  border-left: 2px solid gray;
  border-right: 2px solid gray;
  }

#operation {
  color: orange !important;
}

#result {
  font-size: 24px !important;
}

.result-operation {
  background-color: black;
  color: white;
  text-align: right;
  margin: 0 auto !important;
  padding: 0 !important;
}

.row {
  margin: 0 auto !important;
  height: 70px;
}

#ac {
  display: flex;
  background-color: rgb(172, 57, 57);
  font-weight: bolder;
  color: white;
}

#dividing {
  display: flex;
  background-color: gray;
  font-weight: bolder;
  color: white;
}

#multiple {
  display: flex;
  background-color: gray;
  font-weight: bolder;
  color: white;
}

#text-ac {
  text-align: center !important;
  display: flex;
  justify-content: center !important;
  align-items: center !important;
  margin: 0 auto !important;
}

.internal-buttons {
  border: 1px solid black;
}

.internal-buttons:hover {
  color: black !important;
  font-size: 18px;
}

#row-special {
  height: 140px;
}

#equal {
  display: flex;
  background-color: rgb(0, 68, 102);
  font-weight: bolder;
  color: white;
}

.internal-buttons {
  padding: 0 !important;
  margin: 0 !important;
}

body {
    background-color: lightblue !important;
}
</style>
