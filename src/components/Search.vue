<template>
    <div class="wrapper-search">
        <div class="search">
            <!--            <div class="search-icon">-->
            <!--                <span>Search</span>-->
            <!--            </div>-->
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

<style lang="scss">
.wrapper-search {
    position: absolute;
    top: 3%;
    right: 0;
    input {
        padding: 0;
    }
    label {
        font-weight: 600;
    }
}
</style>