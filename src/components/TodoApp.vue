<template>
  <div class="container">
    <h1 class="text-center mt-5">My todo-app</h1>
<!-- Input-->
<div class="d-flex">
<input v-model="tache" type="text" placeholder="Entrez une tache" class="form-control">
<button @click="submitTaches()" class="btn btn-warning rounded-0"> Ajoutez</button>
</div>
<!--Tables-->
<table class="table">
  <thead>
    <tr >
      <th scope="col" >Taches</th>
      <th scope="col">Evolution</th>
      <th scope="col" class="text-center">Last</th>
      <th scope="col"  class="text-center" >Handle</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(tache,index) in taches" :key="index">
      <th>{{tache.name}}</th>
      <td ><span class="pointer" @click="changeEvolution(index)">{{tache.Evolution}}</span></td>
      <td>
      <div class="text-center" @click="editTache(index)">
      <span class="fa fa-pen"></span>
      </div>
      </td>
      <td><div class="text-center" @click="deleteTache(index)">
      <span class="fa fa-trash"></span></div></td>
    </tr>
   
  
  </tbody>
</table>
</div>
 
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String
  },
  data(){
    return {
      tache:'',
      editedTache:null,
      statusDisponibles:['En cours','A faire', 'Fini'],

      taches:[
        {
          name:'Manger les deux Gateaux',
          Evolution:'Todo'
        },
        {
          name:'Manger les bananes',
          Evolution:'En cours'
        }
      ]
    }
  },


  methods: {
    submitTaches(){
if(this.tache.length== 0) return;

if(this.editedTache==null) {
   this.taches.push({
     name: this.tache,
     Evolution:'En cours'
   });
   }else{
     this.taches[this.editedTache].name= this.tache;
     this.editedTache=null;
   }
this.tache='';

    },
    deleteTache(index){
      this.taches.splice(index,1)
    },
    editTache(index){
      this.tache= this.taches[index].name;
      this.editedTache = index;
    },
    changeEvolution(index){
    let newIndex=  this.statusDisponibles.indexOf(this.taches[index].Evolution);
   if (++newIndex >2)
   newIndex=0;
   this.taches[index].Evolution= this.statusDisponibles[newIndex];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
  cursor:pointer;
}
</style>
