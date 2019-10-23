<template>
  <div class="hello">
    <h2>First-Page  </h2>
    
    
      <ul v-for="data in list" :key="data"> </ul>
     <h3> List ID:  {{idList}} </h3> <br><br>
      <h3> Name List: {{nameList}}</h3> <br><br>
      <h3> Filter Function: {{wordLength}} </h3><br>
      <h3> Find function: {{idFind}} </h3> <br>
      <h3> Reduce Function: {{idReduce}}</h3> <br>
      {{nameForEach}}

    
  </div>
</template>

<script>
// console.log("hdskjgahujfds")
export default {
  name: 'HelloWorld',
  data(){
    return{
      list:[],
      idList:[],
      nameList:[],

    }
  },
  // methods:{
  // getNameList(){
  //   debugger
  //   console.log(this.nameList);
  // }
  // },
   mounted () {
     this.axios
      .get('https://jsonplaceholder.typicode.com/users')
      .then(response =>{ 
        this.list = response.data
        // this.list=this.list.sort()
        this.list.map(x=>this.idList.push(x.id))
       
        this.list.map(x=>{
          this.nameList.push(x.name);
          this.nameList.sort();
          
          
        })
      })
  },computed:{
    wordLength: function(){
     return this.nameList.filter(word => word.length > 17);
    },
    //find number greater than 5.
    idFind: function(){
    return this.idList.find(function(element){
      return element>5 })
      // console.log(idList)
    },
    // Reduce function (sum)  
    idReduce: function(){
      const reducer = (accumulator,currentValue)=> accumulator + currentValue;
       return this.idList.reduce(reducer);
    
    },
    // for Each.
    nameForEach:function(){
    let names = []
     this.nameList.forEach(function(item){
         names.push("This is and element " + item)
      })
    return names.join('###########')
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
