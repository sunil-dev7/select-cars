<template>
  <div>
<label for="years">Year:</label>
<select name="years" id="years">
  <option v-for="y in generateYears()" :key="y" :value="y">{{y}}</option>
</select>
<label for="marks">Mark:</label>
<select name="marks" id="marks" v-model="mark">
  <option v-for="m in marks" :key="m.text" :value="m.text">{{m.text}}</option>
</select>
<label for="models">Model:</label>
<select name="models" id="models">
  <option v-for="m in fetchMarkModels(mark)" :key="m" :value="m">{{m}}</option>
</select>

  </div>
</template>

<script>
export default {
  name: 'SelectAuto',
  props: {
    msg: String
  },
  data() {
    return {
    mark: '',
     marks: [
        { 
         text: 'Volvo',
         models :[
           'XC90',
           'XC60',
           'XC40',
           'S60'
         ]
         },
        { 
          text: 'Mercedese',
           models :[
           'model1',
           'model2',
           'model3',
         ]
          },
        { 
          text: 'Audi',
            models :[
           'audi-m1',
           'audi-m2',
           'audi-m3',
           'audi-m4'
         ] 

          }
      ]
    }
  },
  methods :{
    generateYears: () => {
      const currentYear = new Date().getFullYear();
      let years = [];
      for(let y=1984; y<= currentYear; y++){
        years.push(y);
      }
      return years;
    },

    fetchMarkModels(mark) {
      if(!mark) return [];
      return this.marks.find(m => m.text === mark).models;
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
