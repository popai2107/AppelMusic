<template>
    <div>
        <!--{{photolist}}-->
        <ul>
            <li v-for="photo in photolist" :key="photo.id">
                id {{photo.id}} : title {{photo.title}}
                <img :src="photo.thumbnailUrl">
            </li>
        </ul>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return{
            photolist:null,
            errored:false,
            loading:false,
        };
    },
    
    mounted () {
        axios
        .get('http://jsonplaceholder.typicode.com/photos')
        .then((response) => {
            //this.photolist = response.data; //array 5000 รายการ
            this.photolist = response.data.slice(0,20)     //จาก array 5000 รายการ ตัดให้เหลือ 20 รายการ
        })
        .catch((error) => {
            console.log(error)
            this.errored = true
        })
        .finally(() => this.loading = false)
    },
    
}
</script>

<style>

</style>