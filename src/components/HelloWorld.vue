<template>
  <div>
    <div>{{ title }}</div>
    <SearchForm 
        @search="search"
    />
    <ul>
        <li v-for="(result, index) in results" :key="index">
            <div>
                <a :href="result.url" target="_blank">
                    <img :src="result.images.preview_gif.url" />
                </a>
            </div>
        </li>
    </ul>
  </div>
</template>

<script>
import SearchForm from './SearchForm.vue';
import Axios from 'axios';

export default {
  name: 'Giphy',
  props: {
    msg: String,
  },
    data () {
      return {
        title: 'Search Giphy',
        apiKey: 'mBPy8jQ0bSSz7ZSj9vKjVG4zhDzJ1zDN',
        results: []
      }
    },
    components:{
        SearchForm
    },
    methods: {
        search (searchTerm){
            Axios.get('http://api.giphy.com/v1/gifs/search?q=' + searchTerm + '&api_key='+this.apiKey+'&limit=5')
                .then((response) => {
                    console.log(response.data.data);
                    this.results = response.data.data;
                })
                .catch((err) => {
                    console.log(err);
                });
        }

    },

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
  display: block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
