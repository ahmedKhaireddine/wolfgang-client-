<template>
    <div class="container">
        <div class="row">
            <div class="col-12 col-md-6">
                <img :src="`${article.picture}`" alt="">
            </div>
            <div  class="col-12 col-md-6">
                <h2>{{ article.name }}</h2>
                <h3>{{ article.reference }}</h3>
                <p>{{ article.description }}</p>
                <p><strong>Prix : {{ article.price }} €</strong></p>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    async asyncData({ app, params }){
        const data = await app.$axios.get(`http://localhost:8888/cours-laravel/Wolfgang/public/api/articles/${params.id}`);
        return { article : JSON.parse(JSON.stringify(data.data.data))}
    }
}
</script>
<style scoped>

</style>