<template>
  <div class="wrapper">

    <div class="wrapper-content">
      <section>
        <div class="container">

          <Message v-if="message" :message="message"/>

          <!-- new note -->

          <NewNote :note="note" @addNewNote="addNote" @selectedNote="selectedNote"/>

          <div class="note-header">
            <!-- title -->
            <h1>{{ title }}</h1>

            <!-- search -->
            <Search :value="search" @search="search = $event" placeholder="Find your note" />

            <!-- controls icons -->
            <div class="icons">
              <svg :class="{active: grid}" @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{active: !grid}" @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

          <!-- note list -->
          <p class="no-notes" v-if="notes.length === 0">There are no notes here!</p>
          <Notes :notes="notesFilter" :grid="grid" @removeNote="removeNote" v-else/>

        </div>
      </section>
    </div>

  </div>
</template>

<script>
import Message from '@/components/Message.vue';
import NewNote from '@/components/NewNote.vue';
import Notes from '@/components/Notes.vue';
import Search from '@/components/Search.vue';

export default {
  components: { Message, NewNote, Notes, Search },
  data: () => ({
    title: 'Notes App',
    search: '',
    message: null,
    select: '',
    grid: true,
    note: {
      title: '',
      descr: '',
      type: 'standart'
    },
    notes: [
      {
        title: 'First Note',
        descr: 'Description for First Note',
        date: new Date(Date.now()).toLocaleString(),
        type: 'standart'
      },
      {
        title: 'Second Note',
        descr: 'Description for Second Note',
        date: new Date(Date.now()).toLocaleString(),
        type: 'medium'
      },
      {
        title: 'Third Note',
        descr: 'Description for Third Note',
        date: new Date(Date.now()).toLocaleString(),
        type: 'important'
      }
    ]
  }),
  computed: {
    notesFilter() {
      let array = this.notes,
          search = this.search;

      if (!search) return array;

      // Search string to lower case
      search = search.trim().toLowerCase();

      // Filter
      array = array.filter(item => {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });

      // Error
      return array;
    }
  },
  methods: {
    addNote() {
      let {title, descr, type} = this.note;

      if (title === '') {
        this.message = 'Title can`t be blank!';
        return;
      }

      this.notes.push({ title, descr, date: new Date(Date.now()).toLocaleString(), type });
      this.message = null;
      this.note.title = '';
      this.note.descr = '';
      this.note.type = 'standart';
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
    selectedNote() {

    }
  }

}
</script>

<style lang="scss">
  .no-notes {
    text-align: center;
    margin-top: 40px;
    font-size: 40px;
  }
</style>