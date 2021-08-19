<template>
  <div class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0">
  <nav class="navbar navbar-expand-lg ">
  <input  
  type="text" 
  placeholder="search.."
  v-model="citySearch"
  > 
  <button class="btn btn-primary" v-on:click="getData">search</button>
  </nav>

    <div class="container">
    <table class="table">
        <thead>
          <tr>
            <th scope="col">Id</th>
            <th scope="col">Title</th>  
            <th scope="col">Location_type</th>
            <th scope="col">lat-long</th>
            <th scope="col">Days</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="p in cityResult" :key="p.id">
              <td>{{p.Key}}</td>
              <td>
                {{p.LocalizedName}}
              </td>
              <td>
                {{p.AdministrativeArea.EnglishName}}
              </td>
              <td>{{p.GeoPosition.Longitude}},{{p.GeoPosition.Latitude}}</td>
              <td>
                <select name="days" id="days" v-on:change="goto($event, p.Key)"
>
                  <option value="1day">1 Days</option>
                  <option value="5day" >5 Days</option>
                  <option value="10day">10 Days</option>
                  <option value="15day">15 Days</option>
                </select>
              </td>
            </tr>
        </tbody>
    </table>
    </div>
  </div>
</template>
<script>
import days from '../pages/days.vue';
export default {
  components:{
    days
  },
   data (){
     return{
        citySearch:'',
        cityResult:[],
       }
   }, 
   methods :{
    getData: async function(){
  
      console.log(this.citySearch);
      const key = 's6GKrcurx7Fw9IVdr5cYviAEL5oYIdQ8'
       const base = `http://dataservice.accuweather.com/locations/v1/cities/search?q=${this.citySearch}&apikey=${key}`

      const response = await fetch(base)
      const data = await response.json();
      // console.log(data);
      this.cityResult = data;
      console.log(this.cityResult);
    },
    goto(e,Key){
      console.log(e.target.value , Key);
      this.$router.push({name: 'days', query: {days: e.target.value , Key: Key}})
    
    }
   },
}
</script>
<style>
.navbar{
    background-color: aliceblue;
    margin: 10px;
    padding: 10px;
}
.navbar input[type=text]{
    padding: 6px;
  border: none;
  margin-top: 8px;
  font-size: 17px;
  width: 92%;
}
.btn-primary{
    margin: 10px;
    margin-top: 21px;
}
/* tr:hover{
    background-color: rgb(111, 111, 119);
} */
</style>