<template>
    <article class="panel is-primary">
        <p class="panel-heading">
            <button class="button is-light" @click="show_add">
                <strong>Add new</strong>
            </button>
        </p>
        <div class="panel-block">
            <p class="control has-icons-left">
                <input class="input is-primary" type="text" placeholder="Search">
                <span class="icon is-left">
                    <i class="fa fa-search" aria-hidden="true"></i>
                </span>
            </p>
        </div>
        <a class="panel-block is-active" v-for="product,key in listproducts">
            <div class="column is-9">
                <span class="panel-icon">
                <i class="fa fa-book" aria-hidden="true"></i>                    
                </span>
                <span class="panel-text">{{product.name}}</span>
            </div>
            <div class="column is-1">
                <span class="panel-icon">
                <i class="has-text-danger fa fa-trash" aria-hidden="true" @click='delete_product(key,product.id)'></i>                
            </span>            
            </div>  
            <div class="column is-1">
                <span class="panel-icon">
                <i class="fa fa-edit" aria-hidden="true" @click="edit_product(key)"></i>                
            </span>            
            </div>  
            <div class="column is-1">
                <span class="panel-icon is-danger">
                <i class="has-text-info fa fa-eye" aria-hidden="true" @click="show_product(key)"></i>                
            </span>            
            </div>               
        </a>
        <Add :openmodal='addActive' @closeRequest='close'></Add>
        <Show :openmodal='showActive' @closeRequest='close'></Show>
        <Edit :openmodal='editActive' @closeRequest='close'></Edit>
    </article>
</template>
<script>
let Add = require('./Add.vue').default;
let Show = require('./Show.vue').default;
let Edit = require('./Edit.vue').default;
export default {
    components:{Add,Show,Edit},
    data(){
        return{
            addActive : '',
            showActive:'',
            editActive:'',
            listproducts:{}
        }
    },
    created(){        
        axios.post('/getproducts')
        .then((response)=>this.listproducts=response.data)
        .catch((error) => this.errors=error.response.data.errors)
    },
    methods:{
        show_add(){
            this.addActive='is-active';
        },
        close(){
            this.addActive=this.showActive=this.editActive='close';
        },
        show_product(key){
            this.$children[1].product=this.listproducts[key];
            this.showActive='is-active';
        },
        edit_product(key){
            this.$children[2].product=this.listproducts[key];
            this.editActive='is-active';
        },
        delete_product(key,id){
            if(confirm('Are you sure?')){
                axios.delete('/product/'.concat(id))
                .then(this.listproducts.splice(key,1))
                .catch();
            }
        }
    }
}
</script>