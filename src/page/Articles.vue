<script>    
    import Table from '../components/Table.vue';
    const Articles = {
    data() {
        return {
            articles: [
                {
                    id: 1,
                    nombre: "Javon",
                    precio: 25,
                    stock: 5
                },
                {
                    id: 2,
                    nombre: "Arroz",
                    precio: 24,
                    stock: 10
                },
                {
                    id: 3,
                    nombre: "Pepsi",
                    precio: 30,
                    stock: 15
                }
            ],
            nombre: '',
            precio: 0,
            stock: 0,
            id: 0
        };
    },
    methods: {
        save(){
            let article = {
                id: this.articles.length + 1,
                nombre: this.nombre,
                precio: this.precio,
                stock: this.stock
            }
            this.articles.push(article);
        },
        deleteArticle(id){
            this.articles = this.articles.filter(element => element.id !== id);
        },
        modify(){
            let index = `${this.id - 1}`;
            this.articles[index].nombre = this.nombre;
            this.articles[index].precio = this.precio;
            this.articles[index].stock = this.stock;
            this.id = 0;
        },
        togleModifyArticle(id){
            let article = this.articles.filter(element => element.id === id);
            this.nombre = article[0].nombre;
            this.precio = article[0].precio;
            this.stock = article[0].stock;
            this.id = id;
        }
    },
    components: { Table }
}
 export default Articles;
</script>

<template>
    <form class="form-control p-5 m-3" @submit.prevent="() => id === 0 ? save() : modify()">
        <div class="mb-3">
            <label class="form-label" for="nombre">Nombre</label>
            <input type="text" class="form-control" id="nombre" v-model="nombre">
        </div>
        <div class="mb-3">
            <label class="form-label" for="precio">Precio</label>
            <input type="number" class="form-control" id="precio" v-model="precio">
        </div>
        <div class="mb-3">
            <label class="form-label" for="stock">Stock</label>
            <input type="number" class="form-control" id="stock" v-model="stock">
        </div>
        <button type="submit" class="btn btn-primary">{{id === 0 ? 'Crear articulo' : 'Modificar articulo'}}</button>
        <button type="button" class="btn btn-secondary" v-show="id !== 0" @click="() => id = 0">Cancelar</button>
    </form>
    <Table :fields="Object.keys({id: 0, nombre: '', precio: 0, stock: 0})" :togleModifyItem="togleModifyArticle" :deleteItem="deleteArticle" :data="articles" />
</template>

