<template>
    <div class="wrapper-new-notes">
        <div class="new-note">
            <label for="title"></label>
            <input type="text" id="title" v-model="titleNote" placeholder="title">
            <label for="descr"></label>
            <textarea id="descr" v-model="descr" placeholder="note text"></textarea>
            <button class="btn" @click="onAddNote"> New Note</button>
        </div>
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