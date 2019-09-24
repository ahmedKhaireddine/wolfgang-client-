<template>
    <div>
        <h2>
            Ajouter un produit
        </h2>
        <form @submit="submit" enctype="multipart/form-data">
            <div>
                <label for="name">Nom de produit</label>
                <input type="text" name="name" id="name" placeholder="Entrez le nom du produit" required v-model="name">
            </div>
            <div>
                <label for="reference">Référence de produit</label>
                <input type="text" name="reference" id="reference" placeholder="Entrez la référence du produit" required v-model="reference">
            </div>
            <div>
                <label for="picture">Photo du produit</label>
                <input type="file" id="picture" @change="previewFiles" multiple>
            </div>
            <div>
                <label for="price">Prix du produit</label>
                <input type="text" name="price" id="price" placeholder="Entrez le prix du produit" required v-model="price">
            </div>
            <div>
                <label for="description">Description du produit</label>
                <textarea name="description" id="description" cols="30" rows="10" placeholder="Entrez la description du produit" required v-model="description"></textarea>
            </div>
            <div>
                <input type="submit" valeur="Valider">
                <nuxt-link :to="`/`">Annuler</nuxt-link>
            </div>
        </form>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                name: '',
                reference: '',
                picture: [],
                price:'',
                description:'',
            }
        },
        methods:{
            previewFiles(event) {
                this.picture = event.target.files[0];
            },
            async submit(e){
                e.preventDefault();
                const article = {
                    name:this.name,
                    reference: this.reference,
                    picture: this.picture,
                    price: this.price,
                    description:this.description,
                }
                console.log('new article',article);
                const data = await this.$axios.post(`http://localhost:8888/cours-laravel/Wolfgang/public/api/articles`, article);
                // console.log('data retour',data);
            }
        }
    }
</script>

