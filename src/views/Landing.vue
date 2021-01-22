<template>
    <div id="landing">
        <h1 id="title-1">TONG KEMIN</h1>
        <slider class="slider"></slider>
        <h1 id="title-2">TONG KEMIN</h1>
    </div>
</template>

<script>
import Slider from "../components/Slider.vue"
    export default {
        components: {
            Slider,
        },
        mounted () {
            if(this.$store.state.artworks.length == 0) {
                this.$store.dispatch("getAllArtworks")
            };
        },
    }
</script>

<style lang="scss" scoped>
#landing {
    width: 100%;
    min-height: 100vh;
    display: grid;
    justify-items: center;
    align-items: center;
    background-color: black;

    #title-1 {
        position: absolute;
        top: 15vh;
        z-index: 100;
        color: white;
        transform: rotate(90deg);
        font-size: 2em;
        left: -25vw;
        text-shadow: 1px 1px 1px black;
    }
    
    .slider {
        width: 100%;
    }

    #title-2 {
        position: fixed;
        z-index: 100;
        color: white;
        transform: rotate(-90deg);
        right: -25vw;
        bottom: 15vh;
        text-shadow: 1px 1px 1px black;
    }
}

@media only screen and (min-width: 600px) {
    #landing {

    #title-1 {
        position: absolute;
        top: 14vh;
        z-index: 100;
        color: white;
        transform: rotate(90deg);
        font-size: 3em;
        left: -18vw;
        text-shadow: 1px 1px 1px black;
    }
    
    .slider {
        width: 100%;
    }

    #title-2 {
        position: fixed;
        z-index: 100;
        color: white;
        transform: rotate(-90deg);
        font-size: 3em;
        right: -18vw;
        bottom: 14vh;
        text-shadow: 1px 1px 1px black;
    }
}
}

@media only screen and (min-width: 1024px) {
    #landing {

    #title-1 {
        position: fixed;
        top: 91vh;
        z-index: 100;
        color: white;
        transform: rotate(0deg);
        font-size: 3rem;
        left: 1vw;
        text-shadow: 3px 3px 3px black;
        letter-spacing: 5px;
    }
    
    .slider {
        width: 100%;
        height: 100vh;
    }

    #title-2 {
        position: fixed;
        z-index: 100;
        color: white;
        transform: rotate(0deg);
        font-size: 3em;
        right: 1vw;
        top: 1vh;
        text-shadow: 3px 3px 3px black;
        letter-spacing: 5px;
    }
}
}
</style>