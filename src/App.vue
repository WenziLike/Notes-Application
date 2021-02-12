<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <div class="wrapper-header">
                        <!-- ================ header-->
                        <div class="wrapper-title">
                            <div class="header">
                                <div class="title">
                                    <h1>{{ title }}</h1>
                                    <div class="sub-title">
                                        <span>{{ subTitle }}</span>
                                        <span class="name">{{ name }}</span>
                                    </div>
                                </div>
                                <!-- ===============  Message-->
                                <message v-if="message" :message="message"/>
                            </div>
                        </div>
                        <!-- ===============  Search-->
                        <search
                            :placeholder="placeholder"
                            :value="search"
                            @search="search = $event">
                        </search>
                        <!-- ===============  Priority-->
                        <priority :valueSelect="priorityDefault"
                                  @onPriority="priority"
                        ></priority>
                    </div>
                    <!-- ===============  icons-->
                    <div>
                        <div class="icons">
                            <span :class="{active:grid}" @click="grid = true">GRID /</span>
                            <span :class="{active:!grid}" @click="grid = false">LINE</span>
                        </div>
                    </div>
                    <div class="wrapper-body">
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
import Priority from '@/components/Priority'

export default {
    data() {
        return {
            priorityDefault: 'none',
            search: '',
            title: 'Notes App',
            name: 'Wenzi',
            subTitle: 'GreatLine',
            placeholder: 'Find your note',
            message: null,
            grid: true,
            note: {
                titleNote: '',
                descr: ''
            },
            notes: [
                {
                    titleNote: 'First Note',
                    descr: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit.',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'green'
                },
                {
                    titleNote: 'Second Note',
                    descr: 'Consequatur illo, tempora.',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'none'
                },
                {
                    titleNote: 'Third Note',
                    descr: '2021 years plans',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'red'
                },
                {
                    titleNote: 'Fourth Note',
                    descr: 'Clicked',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'blue'
                },
                {
                    titleNote: 'Fifth Note',
                    descr: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. ' +
                        'Consequatur illo, tempora.' +
                        ' Accusamus doloremque eligendi ' +
                        'et inventore omnis similique sint vero.',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'none'
                },
                {
                    titleNote: 'Sixth Note',
                    descr: 'Weather not bad',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'none'
                },
                {
                    titleNote: 'Book',
                    descr: 'Accusamus doloremque eligendi et inventore omnis similique sint vero.',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'none'
                }
            ]
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
                date: new Date(Date.now()).toLocaleString(),
                priority: this.priorityDefault
            })
            this.titleNote = ''
            this.descr = ''
            this.message = null
            console.log(this.notes)
        },
        removeNote(index) {
            this.notes.splice(index, 1)
        },
        priority(value) {
            this.priorityDefault = value
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
        Search,
        Priority
    }
}
</script>

<style lang="scss">
#app {
    .none {
        border-left: 0.6em #ffffff solid;
    }
    .red {
        border-left: 0.6em #ec0404 solid;
    }
    .yellow {
        border-left: 0.6em yellow solid;
    }
    .green {
        border-left: 0.6em greenyellow solid;
    }
    .blue {
        border-left: 0.6em #0077ff solid;
    }
    .full.red {
        border-left: 1.6em #ec0404 solid;
    }
    .full.yellow {
        border-left: 1.6em yellow solid;
    }
    .full.green {
        border-left: 1.6em greenyellow solid;
    }
    .full.blue {
        border-left: 1.6em #0077ff solid;
    }
}
</style>
