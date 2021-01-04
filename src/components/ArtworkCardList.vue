<template>
<div>
    <artwork-card class="artworks" v-for="art in arts" :key="art.id" :art="art" @deleteArt="deleteArt"></artwork-card>
    <div class="spacer"></div>
    <div class="pagination">
        <div></div>
        <button @click="previous" v-if="this.currentPage != 1">Previous</button>
        <button @click="next" v-if="this.currentPage != this.totalPages">Next</button>
        <div></div>
    </div>
</div>
</template>

<script>
import ArtworkCard from "../components/ArtworkCard.vue";
import axios from "axios";

export default {
    name: "artwork-card-list",
    components: {
        ArtworkCard,
    },
    data() {
        return {
            currentPage: 1,
            offset_value: 0,
            arts: [],
            display: false,
        };
    },
    methods: {
        deleteArt: function (data) {
            console.log(data);
            for (let i = 0; i < this.$store.state.artworks.length; i++) {
                if (this.$store.state.artworks[i].id == data) {
                    this.$store.state.artworks.splice(i, 1);
                }
            }
        },
        firstPage: function () {
            axios
                .request({
                    url: "https://artisttongkemin.ml/api/artwork",
                    method: "GET",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    params: {
                        offset_value: 0,
                    },
                })
                .then((response) => {
                    console.log(response);
                    this.arts = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        next: function () {
            this.currentPage = this.currentPage + 1;
            axios
                .request({
                    url: "https://artisttongkemin.ml/api/artwork",
                    method: "GET",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    params: {
                        offset_value: (this.currentPage - 1) * 6,
                    },
                })
                .then((response) => {
                    console.log(response);
                    this.arts = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        previous: function () {
            this.currentPage = this.currentPage - 1;
            axios
                .request({
                    url: "https://artisttongkemin.ml/api/artwork",
                    method: "GET",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    params: {
                        offset_value: (this.currentPage - 1) * 6,
                    },
                })
                .then((response) => {
                    console.log(response);
                    this.arts = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    },
    computed: {
        totalPages: function () {
            if (this.$store.state.artworks.length == 0) return;
            console.log(this.$store.state.artworks.length);
            return Math.ceil(this.$store.state.artworks.length / 6);
        }
    },
    mounted() {
        this.$store.dispatch("getAllArtworks");
        this.firstPage();
    },
};
</script>

<style lang="scss" scoped>
.artworks {
    min-height: 5vh;
    width: 90%;
}

.pagination {
    width: 100%;
    height: 10vh;
    display: grid;
    grid-template-columns: 15% 35% 35% 15%;
    column-gap: 1.5vw;
    justify-items: center;
    align-items: center;
    margin-bottom: 1em;

    button {
        width: 80%;
        height: 5vh;
        border: 1px solid black;
        border-radius: 1em;
        background-color: white;
        font-size: 1rem;
        font-weight: bold;

        :hover {
            background-color: lightgrey;
        }
    }
}

@media only screen and (min-width: 1024px) {
    .artworks {
        width: 90%;
        display: grid;
    }

    .spacer {
        width: 100%;
    }

    .pagination {
        width: 100%;
        height: 10vh;
        display: grid;
        grid-template-columns: 0 1fr 1fr 0;
        column-gap: 1.5vw;
        justify-items: center;
        align-items: center;
        margin: 1em 0 1em 0;

        button {
            width: 60%;
            height: 5vh;
            border: 1px solid black;
            border-radius: 1em;
            background-color: white;
            font-size: 1rem;
            font-weight: bold;

            :hover {
                background-color: lightgrey;
            }
        }
    }
}
</style>
