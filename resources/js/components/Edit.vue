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
                        <input class="input" type="text" :class="{'is-danger':errors.name}" placeholder="Name" v-model="product.name">
                    </div>
                    <p class="help is-danger" v-if="errors.name" v-for="err in errors.name">{{err}}</p>
                </div>

                <div class="field">
                    <label class="label">Price</label>
                    <div class="control">
                        <input class="input" type="number" :class="{'is-danger':errors.price}" placeholder="Text input" v-model="product.price">
                    </div>
                    <p class="help is-danger" v-if="errors.price" v-for="err in errors.price">{{err}}</p>
                </div>

                <div class="field">
                    <label class="label">Description</label>
                    <div class="control">
                        <textarea class="textarea" :class="{'is-danger':errors.description}" placeholder="Textarea" v-model="product.description"></textarea>
                    </div>
                    <p class="help is-danger" v-if="errors.description" v-for="err in errors.description">{{err}}</p>
                </div>
            </section>
            <footer class="modal-card-foot">
                <button class="button is-success" @click="editproduct">Edit product</button>
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
                product:{},                
                errors:{}
            }
        },
        methods: {
            close() {
                this.$emit('closeRequest')
            },
            editproduct() {
                axios.put('/product/'.concat(this.product.id),this.$data.product)
                .then((response)=>this.close())
                .catch((error) => this.errors=error.response.data.errors);
                                         
            }
        }
    }
</script>