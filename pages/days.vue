<template>
  <div class="container">
      <button @click="getDaysData" >click</button>
      <h1 v-for="k in Key" :key="k.id">
          {{k}}
      </h1>
  </div>
</template>

<script>
export default {
    data(){
        return{
            Key: []
        }
    },
    props: ['days'],
    
    methods: {
        getDaysData: async function(){
            console.log(this.$router)
            const {days, Key} = this.$router.history.current.query;
            const key = 's6GKrcurx7Fw9IVdr5cYviAEL5oYIdQ8'
       const base = `http://dataservice.accuweather.com/forecasts/v1/daily/${days}/${Key}?apikey=s6GKrcurx7Fw9IVdr5cYviAEL5oYIdQ8`

      const response = await fetch(base)
      const data = await response.json();
      // console.log(data);
      this.Key = data;
      console.log(this.Key);
    },
    }
}
</script>

<style>

</style>