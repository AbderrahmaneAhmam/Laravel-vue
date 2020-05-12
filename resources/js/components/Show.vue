<template>
    <div class="modal" :class='openmodal'>
        <div class="modal-background" @click="close"></div>
        <div class="modal-card">
            <header class="modal-card-head">
                <p class="modal-card-title">Add product</p>
                <button class="delete" aria-label="close" @click="close"></button>
            </header>
            <section class="modal-card-body">
                <div class="field">
                    <label class="label">Name</label>
                    <div class="control">
                        <p>{{listproducts.name}}</p>
                    </div>                    
                </div>

                <div class="field">
                    <label class="label">Price</label>
                    <div class="control"> 
                        <p>{{listproducts.price}}</p>                       
                    </div>                    
                </div>

                <div class="field">
                    <label class="label">Description</label>
                    <div class="control"> 
                        <p>{{listproducts.description}}</p>                       
                    </div>                    
                </div>
            </section>
            <footer class="modal-card-foot">                
                <button class="button" @click="close">Cancel</button>
            </footer>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['openmodal'],
        data() {
            return{
                listproducts:''
            }
        },
        methods: {
            close() {
                this.$emit('closeRequest')
            }
        }
    }

</script>

<style>

</style>
