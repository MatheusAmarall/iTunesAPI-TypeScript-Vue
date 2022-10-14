<template>
    <div>
        <h3>Album Name: {{album.collectionName}}</h3>
        <h5>ArtWork</h5>
        <img :src="album.artworkUrl100" alt="">
        <h5>Price: {{album.collectionPrice}}</h5>
    </div>
</template>

<script lang="ts">
import { Result } from '../types/itunesTypes.interface';
import { defineComponent, PropType } from 'vue'

export default defineComponent({
    props: {
        album: {
            type: Object as PropType<Result>,
            required: true
        }
    }
})
</script>

<style lang="sass" scoped>

</style>
