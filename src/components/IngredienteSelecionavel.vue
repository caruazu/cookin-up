<script lang="ts">
import Tag from './Tag.vue';

export default{
    components: {Tag},
    emits: ['adicionarIngrediente', 'removerIngrediente'],

    props:{
        ingrediente: {
            type: String,
            required: true
        },
    },
    data() {
        return {
            selecionado: false
        }
    },
    methods:{
        aoClicar(){
            this.selecionado = !this.selecionado;

            if(this.selecionado){
                this.$emit('adicionarIngrediente', this.ingrediente);   
            } else {
                this.$emit('removerIngrediente', this.ingrediente);
            }
        }
    }
    
}
</script>

<template>
    <button class="ingrediente" v-on:click="aoClicar">
        <Tag v-bind:texto="ingrediente" :ativa="selecionado"/>
    </button>
</template>

<style scoped>
.ingrediente{
    cursor: pointer;
}
</style>