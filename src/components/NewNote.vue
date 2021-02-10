<template>
    <div class="new-note">
        <label for="title"></label>
        <input type="text" id="title" v-model="titleNote">
        <label for="descr"></label>
        <textarea id="descr" v-model="descr"></textarea>
        <button class="btn" @click="onAddNote"> New Note</button>
    </div>

</template>

<script>

export default {
    emits: ['onAddNote'],

    data() {
        return {
            titleNote: '',
            descr: ''
        }
    },
    methods: {
        onAddNote() {
            this.$emit('onAddNote', {
                titleNote: this.titleNote,
                descr: this.descr
            })
            this.titleNote = ''
            this.descr = ''
        }
    }
}
</script>
<style lang="scss">
.new-note {
    .btn {
        margin-top: 2%;
        display: inline-block;
        padding: 0.8em 4em;
        line-height: 1;
        text-transform: uppercase;
        font-weight: 900;
        cursor: pointer;
        border-radius: 20px;
        box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);

        &:hover {
            color: #2c3e50;

        }

        &:active {
            box-shadow: none;
            text-transform: none;
        }
    }
}
</style>