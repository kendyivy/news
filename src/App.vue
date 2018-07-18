<template>
  <div class="container">
  <div class="topnav">
          <a class="active" href="#search">search</a>
            
            <input  v-model="search"type="text" placeholder="Search..">
            
            <button v-on:click="loadNews"type="button">Search</button>
            <p v-if="loading">Please wait...</p>
            
        </div>
        <div class="loader" v-if="loading"></div>
   <div v-for="article in news">

      <img  v-if="article.urlToImage" :src="article.urlToImage" alt=""> 
     <h3>{{article.title}}</h3>
     <div> class="column"
     <h4>{{article.author}}</h4></div>

     <blockquote>
     <p>{{article.description}}</p>
     </blockquote>
    <a href :"article.url"target="blank" class="button">Read More</a>



    </div>

  </div>
</template>

<script>
import axios from 'axios'

const baseUrl = "https://newsapi.org/v2/";
const apiKey="98b4d0418d994067b20bc487a55d994e";
const endpoint= "/everything";


const data={
news:[],
search: '',
loading:false
}
export default {
  data: function() {
    return  data
      
  },
  created(){
    this.loadNews();
  },
  methods: {
  	loadNews(){
     if(this.search.length<1){
      return;
     }
     
     this.loading = true;
     this.news = [];


     let url=baseUrl + endpoint + '?q=' + this.search + '&apiKey=' + apiKey;


    axios.get(url).then(function(response){
    console.log(response.data.articles)
    data.loading = false;
    data.news=response.data.articles
    }).catch(function(error) {
    console.log(error.message)
    })
    }
  
  }
}
</script>
