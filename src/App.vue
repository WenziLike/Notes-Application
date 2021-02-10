<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <!-- ===============  Search-->
                    <search
                        :placeholder="placeholder"
                        :value="search"
                        @search="search = $event">
                    </search>
                    <!-- ================ header-->
                    <h1>{{ title }}</h1>
                    <span class="name">{{ name }}</span>
                    <div class="sub-title">
                        <span>{{ subTitle }}</span>
                    </div>
                    <!-- ===============  icons-->
                    <div>
                        <div class="icons">
                            <span :class="{active:grid}" @click="grid = true">GRID /</span>
                            <span :class="{active:!grid}" @click="grid = false">LINE</span>
                        </div>
                    </div>
                    <!-- ===============  Message-->
                    <message v-if="message" :message="message"/>
                    <!-- ===============  New Notes-->
                    <new-note @onAddNote="addNote"/>
                    <!-- ===============  Delete And Notes-->
                    <notes
                        v-if="notes.length"
                        :notes="notesFilter"
                        :grid="grid"
                        @onRemoveNote="removeNote"/>
                    <div v-else>
                        <h2 class="no-notes">No Notes</h2>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
import Message from '@/components/Message'
import NewNote from '@/components/NewNote'
import Notes from '@/components/Notes'
import Search from '@/components/Search'

export default {
    data() {
        return {
            search: '',
            title: 'Notes App',
            name: 'wenzi',
            subTitle: 'GridLine',
            placeholder: 'Find your note',
            message: null,
            grid: true,

            note: {
                titleNote: '',
                descr: ''
            },
            notes: []
        }
    },
    methods: {
        addNote({ titleNote, descr }) {
            if (titleNote === '') {
                this.message = 'title can\'t be blank... !!!'
                return false
            }

            this.notes.push({
                titleNote,
                descr,
                date: new Date(Date.now()).toLocaleString()
            })
            this.titleNote = ''
            this.descr = ''
            this.message = null
        },
        removeNote(index) {
            this.notes.splice(index, 1)
        }
    },
    computed: {
        notesFilter() {
            let array = this.notes
            let search = this.search
            if (!search) return array
            search = search.trim().toLowerCase()
            array = array.filter(function (item) {
                if (item.titleNote.toLowerCase().indexOf(search) !== -1) {
                    return item
                }
            })
            return array
        }
    },
    components: {
        Notes,
        Message,
        NewNote,
        Search
    }
}
</script>

<style lang="scss">
#app {
    section {
        padding: 0;
    }
    h1 {
        display: inline-block;
        text-shadow: 4px 4px 10px rgba(0, 0, 0, 0.6);
    }
    span.name {
        display: inline-block;
        padding-left: 0.5%;
    }
    .container {
        textarea,
        input {
            display: block;
            //background-color: #ffffff;
            border: none;
            border-bottom: #00aced 3px solid;
            min-width: 50%;
            height: 40px;
            padding: 5px 10px 5px 10px;
            font-size: 16px;
            outline: none;
            border-radius: 2px;
        }
        textarea {
            position: relative;
            z-index: 2;
            margin-top: 2%;
            height: 50px; /* Высота поля в пикселах */
            resize: none; /* Запрещаем изменять размер */
            border: #00aced 1px solid;
            box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
        }
        div.sub-title {
            position: absolute;
            top: 56px;
            left: -10px;
        }
        .icons {
            position: absolute;
            top: 240px;
            left: 40%;
            cursor: pointer;
            z-index: 1;
            span {
                margin: 5px;
                color: #2c2c2c;
                font-weight: 900;
                &.active {
                    color: #8854d0;
                }
            }
        }
        .no-notes {
            text-align: center;
            font-weight: 900;
            font-size: 2em;
            margin-top: 10%;
        }
    }
}
</style>
