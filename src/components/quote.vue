<template>
    <div class="quote">
            {{this.displayQuote}}
    </div>
</template>

<script>
    export default {
        props: {
            displayQuote: {
                type: String,
                required: true,
                default: null,
            }
        },
    }
</script>

<style scoped>
    .quote {
        margin: 6rem auto;
        font-size: 2rem;
        max-width: 70%;
    }
</style>
