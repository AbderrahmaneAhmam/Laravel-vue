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
        <a class="panel-block is-active">
            <div class="column is-9">
                <span class="panel-icon">
                <i class="fa fa-book" aria-hidden="true"></i>                    
                </span>
                <span class="panel-text">bulma</span>
            </div>
            <div class="column is-1">
                <span class="panel-icon">
                <i class="has-text-danger fa fa-trash" aria-hidden="true"></i>                
            </span>            
            </div>  
            <div class="column is-1">
                <span class="panel-icon">
                <i class="fa fa-edit" aria-hidden="true"></i>                
            </span>            
            </div>  
            <div class="column is-1">
                <span class="panel-icon is-danger">
                <i class="has-text-info fa fa-eye" aria-hidden="true"></i>                
            </span>            
            </div>               
        </a>
        <Add :openmodal='addActive' @closeRequest='close'></Add>
    </article>
</template>
<script>
let Add = require('./Add.vue').default;
export default {
    components:{Add},
    data(){
        return{
            addActive : ''
        }
    },
    methods:{
        show_add(){
            this.addActive='is-active'; 
        },
        close(){
            this.addActive='close';
        }
    }
}
</script>