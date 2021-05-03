<template>
    <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
        <div class="twoot-username">
             {{ username }}
        </div>
        <div class="twoot-content">
            {{twoot.id}} {{ twoot.content}}
        </div>
    </div>
</template>

<script>
    export default {
        name: "TwootItem",
        props: {
            username: {
                type: String,
                required: true,
            },
            twoot: {
                type: Object,
                required: true
            }
        },
        methods:{
            favouriteTwoot( id ){
                this.$emit('favourite', id )
            }
        }
    }
</script>

<style scoped>

</style>
