<template>
    <div class="notes">
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

<style lang="scss">
.notes {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    margin-top: 2%;
    .note {
        margin: 0.5%;
        min-width: 30%;
        height: 100%;
        overflow: hidden;
        padding: 1rem;
        border-radius: 0 4px 4px 0;
        box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
        background: #fff;
        transition: all .25s cubic-bezier(.02, .01, .47, 1);
        &-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            h3 {
                margin: 0;
                font-weight: 700;
                font-style: italic;
                text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.6);
            }
            .delete {
                font-size: 1.8em;
                cursor: pointer;
                &:hover {
                    color: #2c2c2c;
                }
            }
        }
        &-body {
            p {
                font-weight: 500;
                color: #273164;
            }
            span {
                color: #999999;
            }
        }
        &.full, &-header {
            h3 {
                display: block;
                margin: 0 auto;
            }
            text-align: center;
            min-width: 100%;
            &span.delete {
                margin-left: 20px;
            }
        }
        &:hover {
            transform: translate(0, -6px);
            transition-delay: 0s !important;
        }
    }
}
</style>