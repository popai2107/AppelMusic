<template>
    <div>
        <input type="text" v-model="textSearch" />
        <button @click="searchData()">Search</button>
        <!--{{playList}}-->

        <div v-for="list in playList" :key="list.artistId">
            <b-card-group columns>
                <b-card
                    v-for="list in playList"
                    :key="list.trackID"
                    :title="list.trackName"
                    :img-src="list.artworkUrl60"
                    :img-alt="list.artistName"
                    img-top
                    tag="article"
                    style="max-width: 20rem;"
                    class="mb-2"
                >
                    <b-card-text>
                        {{list.trackId}} : {{list.trackName}}
                        <audio controls>
                            <source :src="list.previewUrl" type="audio/mpeg">
                        </audio>
                    </b-card-text>

                    <b-button :href="list.previewUrl" variant="primary">Go somewhere</b-button>
                </b-card>
            </b-card-group>
        </div>        
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            playList:null,
            textSearch:"",
        };
    },
    methods: {
        searchData(){
            axios
            .get('https://itunes.apple.com/search?term='+this.textSearch+'&limit=10')
            .then((response) =>{
                this.playList = response.data.results
            })
            .catch((err)=> {
                console.log(err)
            })
        },
    },
    

}
</script>

<style>

</style>