<template>
    <div class="wrapper-priority">
            <div class="priority">
                <label for="priority">Priority</label>
                <select id="priority" v-model="priority">
                    <option value="none">None</option>
                    <option value="blue">Not urgent and not important</option>
                    <option value="green">Urgent and not important</option>
                    <option value="yellow">Not urgent and not important</option>
                    <option value="red">Urgent and important</option>
                </select>
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