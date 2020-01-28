<template>
  <v-app>
    <v-app-bar 
      app
      color="green"
      dark
      floating
    >
      <v-toolbar-title>
        SHP-News
      </v-toolbar-title>
    </v-app-bar>

    <v-content class="pa-5 pt-12">
      <v-container class="mt-12">
        <v-row>
          <v-col 
            cols="12" 
            md="6"
            lg="3"
            v-for="(article, index) in articles"
            :key="index"
          >
            <v-card>
              <img :src="article.urlToImage" style="width: 100%">
              <v-card-title>
                {{article.title}}
              </v-card-title>
              <v-card-text>
                {{article.description}}
              </v-card-text>
              <v-card-actions>
                <v-btn class="ma-2" outlined color="green" :href="article.url" target="_blank">
                  <v-icon>mdi-link-variant</v-icon> Читать в источнике...
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>

        </v-row>

        
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  components: {
  },

  data: () => ({
    articles: []
  }),
  methods: {
    getNews(){
      this.axios.get('http://188.225.47.187/api/news/get_top_headlines.php')
        .then( (response)=>{
          window.console.log(response);
          this.articles = response.data.articles;
        } )
    }
  },
  mounted(){
    this.getNews();
  }
};
</script>
