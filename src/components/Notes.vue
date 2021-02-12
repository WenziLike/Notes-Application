<template>
    <div class="wrapper-notes">
        <div class="note"
             v-for="(note,index) in notes"
             :key="note"
             :class="[{
                 full:!grid,
             } , note.priority]">
            <div class="note-header" :class="{full:!grid}">
                <h3>{{ note.titleNote }}</h3>
                <span class="delete" @click="$emit('onRemoveNote',index)">&times;</span>
            </div>
            <div class="note-body">
                <p>{{ note.descr }}</p>
                <span>{{ note.date }}</span>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    emits: ['onRemoveNote'],
    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    }
}
</script>