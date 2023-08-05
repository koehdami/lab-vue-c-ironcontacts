<template>
  <div class="main-container">
    <h2>IronContacts</h2>
    <div class="btn-container">
      <button @click="dataVar.push(insertRandom())">Add Random Contact</button>
      <button @click="dataVar.sort((a, b) => b.popularity - a.popularity)">Sort by popularity</button>
      <button @click="dataVar.sort((a, b) => a.name.localeCompare(b.name))">Sort by name</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="person in dataVar">
          <td>
            <img :src="person.pictureUrl">
          </td>
          <td>{{ person.name }}</td>
          <td>{{ person.popularity }}</td>
          <td v-if="person.wonOscar">🏆</td>
          <td v-else></td>
          <td v-if="person.wonEmmy">🏆</td>
          <td v-else></td>
          <td>
            <button @click="deleteContact(person.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import data from "./contacts.json"
  import { ref } from "vue"
  export default{
    data(){
      return{
        dataSet: data.slice(5),
        dataVar:ref(data.slice(0, 5))
      }
    },
    methods:{
      insertRandom(){
        if(this.dataSet.length !== 0){
          const randomInt = Math.floor(Math.random() * this.dataSet.length)
          const x = this.dataSet[randomInt]
          this.dataSet.splice(randomInt, 1);
          return x;
        }
      },
      deleteContact(id){
        console.log(this.dataVar)
        for(let i = 0; i < this.dataVar.length; i++){
          if(id === this.dataVar[i].id){
            return this.dataVar.splice(i, 1);
          }
        }
      }
    }
  }
</script>

<style>
  table tr{
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
  }
  table th{
    font-size: 23px;
    margin-bottom: 15px;
  }
  table td, table th{
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    flex-wrap: nowrap;
  }
  table img{
    width: 100%;
  }
  .main-container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  h2{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 45px;
    text-align: center;
  }
  .btn-container{
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
  }
</style>
