<template>

    <div class="cardsWrap">
        <span v-show="isSuccess">The operation was a success.</span>
        <span v-show="!isSuccess">The operation failed.</span>
        <v-card
        dark
        max-width="344"
        class="mx-auto v-card"
        v-show="output!=null"
        v-for="(row, index) in output"
        :key="index">
        <v-card-title>
            {{row.name}}
        </v-card-title>
        <v-card-text>
            ID: {{row.item_id}}
        </v-card-text>
        </v-card>
    </div>

</template>

<script>
export default {
    props: {
        isSuccess: Boolean,
        output: Object,
    }
}
</script>

<style scoped>
</style>