<template>
    <div class="card mx-auto">
            <div class="card__image">
                
                <img v-if="info.poster_path" :src="`https://image.tmdb.org/t/p/w342${info.poster_path}`" :alt="info.original_title || info.original_name" class="card__image">
                <div v-else class="card__image__replace">
                    <h5>Ci scusiamo per il disagio, ma non disponiamo del poster di <span class="title">"{{info.original_title || info.original_name}}"</span></h5>
                    <p>Team <span>BOOLFLIX</span></p>
                </div>
            </div>

            <div class="card__info">
                <div><strong>Titolo:</strong> {{info.title || info.name}}</div>
                
                <!-- i use this v-if to avoid showing the title of the show if it is the same as the original one -->
                <div v-if="info.title !== info.original_title || info.name !== info.original_name"><strong>Titolo orginale:</strong> {{info.original_title || info.original_name}}</div>
                
                <div><strong>Lingua:</strong>
                <lang-flag v-if="Object.keys(this.langObj).includes(info.original_language)" :iso="info.original_language" :squared="true"/>
                <font-awesome-icon v-else :icon="questionMark"/>
                </div>
                
                <div><strong>Voto:</strong> <font-awesome-icon class="solid" :icon="starSolid" v-for="elm in starMaker()" :key="elm"/><font-awesome-icon class="empty" :icon="starEmpty" v-for="elm in starDestroyer()" :key="elm"/></div>
                
                <div v-if="info.overview"><strong>Overview:</strong> {{info.overview}}</div>
            </div>
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags'; 
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faStar as fasStar } from '@fortawesome/free-solid-svg-icons';
import { faStar as farStar } from '@fortawesome/free-regular-svg-icons';
import { faQuestion } from '@fortawesome/free-solid-svg-icons';


export default {
    name: 'MovieCard',
    props:['info'],
    components:{
        LangFlag,
        FontAwesomeIcon,
    }, 
    data() {
        return {
            starSolid: fasStar,
            starEmpty: farStar, 
            questionMark: faQuestion,
            minStar: 0,
            maxStar: 5,
            maxVote: 10,
            langObj:{
                am: 'am',
                ar: 'sy',
                az: 'az',
                bn: 'bd',
                be: 'be',
                ca: 'es-ca',
                cs: 'cz',
                de: 'de',
                en: 'gb',
                es: 'es',
                et: 'et',
                fa: 'ir',
                fr: 'fr',
                bg: 'bg',
                ha: 'ng',
                hi: 'in',
                hu: 'hu',
                hy: 'am',
                it: 'it',
                ja: 'jp',
                jv: 'id',
                km: 'km',
                ko: 'kr',
                lv: 'lv',
                mr: 'in',
                ms: 'my',
                pl: 'pl',
                pt: 'pt',
                ro: 'ro',
                ru: 'ru',
                sw: 'ke',
                ta: 'lk',
                te: 'in',
                th: 'th',
                tr: 'tr',
                uk: 'ua',
                uz: 'uz',
                vi: 'vn',
                zh: 'cn',
            }
        }
    },
    methods:{
        consecArrMaker(min, max) {
            const arrStar = [];
            for (let i = min; i < max; i++){
                arrStar.push(i);
            }
            return arrStar;
        },
        starMaker() {
            return this.consecArrMaker(this.minStar, Math.ceil( this.info.vote_average / (this.maxVote / this.maxStar) ));
        },
        starDestroyer(){
            return this.consecArrMaker( Math.ceil( this.info.vote_average / (this.maxVote / this.maxStar) ), this.maxStar );
        }

    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/variables.scss';


    .card{
        position: relative;
        color: #fff;
        max-width: 14rem;
        height: calc(14rem * 1.5);
        background-color: $mainBgColor;

        &__image{
            height: 100%;

            img{
                width: 100%;
                height: 100%;
                object-fit: cover;
            }

            &__replace{
                padding: .625rem;
                background-color: $mainBgColor;
                position: relative;
                height: 100%;

                .title{
                    display: block;
                    font-weight: 700;
                    margin-top: 8px;
                    text-align: center;
                }

                p{
                    text-align: center;
                    position: absolute;
                    right: .875rem;
                    bottom: 3.125rem;
                    font-size: 1.25rem;
                    background-color: $mainBgColor;


                    span{
                        color: $mainTextColor;
                        display: block;
                        font-weight: 900;
                    }
                }
            }
        }


        &__info{
            padding: .625rem;
            position: absolute;
            top:0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            opacity: 0;
            transition: opacity .3s ease-in-out;
            overflow-y: hidden;
            background-color: $mainBgColor;

            &:hover{
                opacity: 1;
                overflow-y: auto;

            }

            .flag-icon{
                margin-left: .5rem;
                border-radius: 50%;
            }

            .solid{
                color: #e7c631;
            }

            .empty{
                color: #9a9a9a
            }
        }
    }

    @media screen and (max-width: 576.1px){
        .card{
            height: calc(320px * 1.5);
            max-width: 320px;

            &__image__replace{
                padding-top: 25px;

            }
        }
    
    }

::-webkit-scrollbar {
    width: 2px;
    }   


</style>