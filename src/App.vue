
<template>
  <div>
    <h1>My to-dos</h1>
      <input id="intext" @keypress.enter = "getTable" 
      placeholder="Create a new to-do..." v-model = "text">    
      <br>
      <br>      
      <table>
          <tr v-for="(item,index) in items" :key="index" >        
            <td  v-if="item.edit===true" >
              <input  type="text"  v-model="item.text" @blur="off(item)" 
              @keypress.enter="$event.target.blur()">                 
            </td>   
             <td v-else>
              {{item.text}}
            </td>
             
            <td>
              <input type="button" value="EDIT" @click ="activeEdit(item)">
            </td>  
           
            <td>
              <input type="button" value="delete" @click ="activeDelete(item)">
            </td>  

          </tr>
      </table>

  </div>

</template>

<script>

export default { 
 data(){
    return{
       text: '',
       items: []
    }
  },
  computed: {
    insertText(){
      return this.text
     }
 }, 
 methods: {    
    getTable(){      
        this.items.push({
            text: this.text,
            edit: false 
        })
    },
    activeEdit: function(item){    
      item.edit = true
    },
    off(item){
      item.edit = false
    },
    activeDelete(item){
      let index = this.items.indexOf(item)
      this.items.splice(index,1)
      /* 
      this.items.pop({
            text: this.text 
        })  */
      /*   let index = this.items.indexOf(item)
        this.items.splice(index,1)*/
    }
  }
 }
</script>

<style>
div{
  margin: auto;
  width: 80%;
  border: 5px;
  padding: 20px;
}

#intext{
  border: 1px solid gainsboro;
  border-radius: 5px;
  width: 40%;
  padding: 5px;
  font-size: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
 table{
  border: 1px solid gainsboro;
  border-radius: 5px;
  width: 40%;
  padding: 30px;
  font-size: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
} 
tr{
border: 1px solid gainsboro;
border-radius: 5px;
  width: auto;
  padding: 20px;
}

body{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#editText{
  border: 0px solid gainsboro;
  border-radius: 5px;
  width: 90%;
  padding: 5px;

}
</style>
