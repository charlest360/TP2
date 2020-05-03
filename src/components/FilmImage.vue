<template>
    <div v-if="filmInfos.image != null  && filmInfos.image.length >0 ">
        <img :src="filmInfos.image" alt="une image" :height="height" :width="width">
    </div>
            
    <div v-else>
        <img src="@/assets/noImage.png" alt="aucune image pour le film" :height="height" :width="width"> 
    </div>
</template>

<script>
    export default {
        props: {
            filmInfos: {
                type: Object,
                default: null,
                required : true
            },
            height : {
                type: Number,
                required : true
            },
            width : {
                type: Number,
                required : true
            }
        },
    }
</script>

<style scoped>

</style>