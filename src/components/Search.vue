<template>
    <div class="wrapper-search">
        <div class="search">
            <label for="Search">Search</label>
            <input type="text" id="Search" :placeholder="placeholder" v-model="search">
        </div>
    </div>
</template>

<script>

export default {
    emits: ['search'],
    props: {
        placeholder: {
            type: String,
            default: 'Search'
        },
        value: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            search: this.value
        }
    },
    watch: {
        search(val) {
            this.$emit('search', val)
            // console.log(val)
        }
    }
}
</script>