<template>
    <div class="searchBox">
        <form v-on:submit.prevent="hitGitHubApi(user_name)">
            <input type="text" placeholder="Nome do usuário" v-model="user_name"/>
            <!-- <input type="submit" value="Enviar"/> -->
        </form>


    <div class="results" v-if="results">
      <img v-bind:src="results.avatar_url" />
      <h2>{{ results.name }}</h2>
      <div>{{ results.bio }}</div>
      <div>{{ results.location }}</div>
      <div v-if="results.followers">Followers: {{ results.followers }}</div>
      <div v-if="results.following">Following: {{ results.following }}</div>
      <a v-if="results.blog" v-bind:href="results.blog">Go to website</a>
      {{ results.message }}
    </div>

    </div>

</template>

<script>
export default {
    name: 'SearchEngine',
    data () {
        return {
        msg: 'Heating engines!',
        user_name: '',
        results: null
        }
    },
    methods: {
        hitGitHubApi(q) {
            let self = this;
            fetch ('https://api.github.com/users/'+ q)
            .then( (j) => {
                return j.json();
            })
            .then( (r) => {
                console.log(r);
                self.results = r;
            })
        }
},

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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

.results img {
    margin-top: 30px;
    float: center;
    width: 250px;
}

</style>
