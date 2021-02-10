<template>
    <div class="wrapper-priority">
        <div class="priority">
            <div class="wrapper-search">
                <label for="priority">Priority:</label>
                <select id="priority" v-model="priority">
                    <option value="none">None</option>
                    <option value="green">Ordinary</option>
                    <option value="yellow">Medium</option>
                    <option value="red">Important</option>
                </select>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    emits: ['onPriority'],
    props: {
        valueSelect: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            priority: this.valueSelect
        }
    },
    watch: {
        priority(value) {
            this.$emit('onPriority', value)
            // console.log(value)
        }
    }
}
</script>

<style lang="scss" scoped>
.wrapper-search {
    top: 10%;
    right: 20%;
    label {
        margin-right: 2%;
    }
    select {
        //border: none;
        outline: none;
        border-radius: .5em;
        option {
            margin: 40px;
            background: rgba(0, 0, 0, 0.3);
            color: #fff;
            text-shadow: 0 1px 0 rgba(0, 0, 0, 0.4);
            option:hover {
                background-color:yellow;
            }
        }
        option[value="green"]{
            background: green;
        }
    }

    select option[value="yellow"] {
        background: yellow;
    }
    select option[value="red"] {
        background-color: #ec0404;
    }
}
</style>