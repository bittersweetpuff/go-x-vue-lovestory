<template>
  <v-container>
    <v-row>

        <v-col cols="12" sm="6">
          <v-text-field
            v-model="num1"
            label="Number 1"
            outlined
            shaped
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="6">
          <v-text-field
            v-model="num2"
            label="Number 2"
            filled
            shaped
          ></v-text-field>
        </v-col>

      </v-row>


      <div class="text-center">
          <v-btn rounded color="primary" dark v-on:click="postreq()">Calculate</v-btn>
      </div>

      <v-row>

          <v-text-field
            v-model="add"
            value=""
            label="Sum"
            filled
            shaped
            disabled
          ></v-text-field>
          <v-text-field
            v-model="sub"
            value=""
            label="Subtraction"
            filled
            shaped
            disabled
          ></v-text-field>
          <v-text-field
            v-model="mul"
            value=""
            label="Multiplication"
            filled
            shaped
            disabled
          ></v-text-field>
          <v-text-field
            v-model="div"
            value=""
            label="Division"
            filled
            shaped
            disabled
          ></v-text-field>

      </v-row>
  </v-container>
</template>

<script>
import axios from 'axios';

  export default {
    name: 'HelloWorld',

      data: function() {
      return {
        add: "", mul: "", sub: "", div: "", 
        num1: "", num2: ""
      }
  },
  methods: {
    postreq: function() {
      var data = {"num1": parseFloat(this.num1), "num2": parseFloat(this.num2)}

            console.log(data) 

      axios({ method: "POST", url: "http://127.0.0.1:8090/calc", data: data, headers: {"content-type": "text/plain" } }).then(result => { 
        this.add = result.data['add']
        this.mul = result.data['mul']
        this.sub = result.data['sub']
        this.div = result.data['div']
      }).catch( error => {
            console.error(error);
      });

    }
  }
  }
</script>
