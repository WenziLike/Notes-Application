<template>
    <h3>{{ message }}</h3>
</template>

<script>
export default {
    props: {
        message: {
            type: String,
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>
h3{
    color: firebrick;
    font-style: italic;
    font-weight: 700;
    text-shadow: 4px 4px 10px rgba(0, 0, 0, 0.6);
}
</style>
