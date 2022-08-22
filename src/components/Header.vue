<template>
    <header class="d-flex justify-content-between align-items-center px-3 py-2">
        <p class="logo">
            BOOLFLIX
        </p>
        <form>
            <input type="text" placeholder="Cerca il film" v-model="searchText">
            <button @click.prevent="$emit('searchMovie', searchText), searchText=''"><font-awesome-icon :icon="searchLens" class="align-middle"/></button>
        </form>
    </header>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faSearch } from '@fortawesome/free-solid-svg-icons';
export default {
    name: 'Header',
    components:{
        FontAwesomeIcon
    },
    data(){
        return{
            searchText:"",
            searchLens: faSearch 
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/variables.scss';


    header{
        height: 4.375rem; 
        position: fixed;
        top:0;
        left: 0;
        width: 100%;
        z-index:2;
        background-color: $mainBgColor;


        p{
            font-weight: 900;
            font-size: 2rem;
            color: $mainTextColor;
            margin: 0;
        }

        input,
        button{
            padding: .125rem .375rem;
            border: none;
            border-radius: .125rem;
            margin-left: 6px;
        }
    }

    @media screen and (max-width: 576.1px){
        input{
            width: 8rem;
        }
    }

</style>