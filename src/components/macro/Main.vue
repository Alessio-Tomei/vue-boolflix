<template>
<main>
    <div class="container">
        <div class="row row-cols-5 gy-3 gx-4">
            <div class="col" v-for="(element, index) in resultList" :key="index">
                <div class="ms_card-box">
                    <div class="ms_poster-container">
                        <img :src="getPoster(element.poster)" alt="">
                    </div>
                    <div class="ms_info-container">
                        <p><span>Titolo: </span>{{element.title}}</p>
                        <p><span>Titolo originale: </span>{{element.originalTitle}}</p>
                        <img class="ms_lang-flag" :src="require(`../../assets/img/${getFlag(element.language)}.jpg`)" alt="">
                        <div class="d-flex">
                            <div class="ms_stars-color" v-for="(star, index) in element.stars" :key="'star'+ index">
                                <i class="fas fa-star"></i>
                            </div>
                            <div v-for="(star, index) in (5 - element.stars)" :key="'star-missing'+ index">
                                <i class="far fa-star"></i>
                            </div>
                        </div>
                        <p><span>Descrizione: </span>{{element.overview}}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</main>
</template>

<script>
export default {
    name: 'Main',
    props: {
        resultList: Array,
    },
    data() {
        return {
            flags: ['it', 'en', 'us', 'es', 'fr'],
            itsHover: false,
        }
    },
    methods: {
        getFlag: function(prefix) {
            let flagPrefix = 'other';
            if (this.flags.includes(prefix)) {
                flagPrefix = prefix;
            }
            return flagPrefix;
        },
        getPoster: function(partialUrl) {
            console.log(partialUrl);
            let posterUrl = require(`../../assets/img/poster-placeholder.png`);
            if (partialUrl != null) {
                posterUrl = `https://image.tmdb.org/t/p/w342${partialUrl}`;
            }
            return posterUrl;
        }
    } 
   
}
</script>

<style lang="scss" scoped>
@import "../../assets/style/variables.scss";

main {
    overflow: auto;
    width: 100%;
    height: calc(100vh - $header-height);
    margin-top: $header-height;
    padding-top: 50px;
    background-color: $bg-light-color;
}

.ms_card-box {
    border: 1px solid white;
    width: 100%;
    padding-top: 150%;
    position: relative;
    top: 0;
    left: 0;
    .ms_poster-container {
    position: absolute;
    top: 0;
    left: 0;
    width:100%;
    height: 100%;
        img {
            width: 100%;
            height: 100%;
        }
    }    
    .ms_info-container {
        display: none;
        overflow: auto;
        position: absolute;
        top: 0;
        left: 0;
        padding: 20px;
        width:100%;
        height: 100%;
        background-color: $bg-color;
        &::-webkit-scrollbar {
            display: none;
        }
        & > * {
            margin-bottom: 10px;
        }
        p {
            span{
                font-weight: bold;
            }
        }
        .ms_lang-flag {
            width: 40px;
            height: 25px;
        }
        .ms_stars-color {
            color: rgb(255, 255, 85);
        }
    } 
    &:hover .ms_info-container{
        display: block;
    }  
}

</style>