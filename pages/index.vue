<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        wolfgang
      </h1>
      <div>
        <h2>Liste de produit: </h2>
        <nuxt-link :to="`products/add`">Ajouter un produit</nuxt-link>
        <ul v-if="articles.length > 0" class="row">
          <li v-for="article in articles" :key="article.id" class="col-12 col-md-6 col-lg-4">
            <img :src="`${article.picture}`"/>
            <h2>{{ article.name }}</h2>
            <nuxt-link :to="`products/${article.id}`">Voir plus de détail</nuxt-link>
          </li>
        </ul>
        <p v-else>Aucune produit pour le moment.</p>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  async asyncData ({ app }) {
    const data = await app.$axios.get(`http://localhost:8888/cours-laravel/Wolfgang/public/api/articles`);
    console.log('data index', data);
    let element = JSON.parse(JSON.stringify(data.data.data));
    console.log('element', element); 
    return { articles: JSON.parse(JSON.stringify(data.data.data)) }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
