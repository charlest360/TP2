<template>
    <div>
        <h2>{{ title }}</h2>
        <ul class="films">
            <li v-for="film in films" :key="film.id">
                <span class="title">{{ film.title }}</span>
                <span class="description">{{ film.description }}</span>
                <span class="rating">{{ film .rating }}</span>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: {
            films : Array
        },
    }
</script>

<style lang="css" scoped>

</style>