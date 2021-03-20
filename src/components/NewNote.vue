<template>
  <div class="new-note">

    <div style="display: flex; align-items: center; justify-content: space-between;">
      <div class="note-block">
        <label>Title</label>
        <input v-model="note.title" type="text" />
      </div>
      <div class="note-block">
        <label>Importance</label>
        <select v-model="note.type">
          <option value="standart">Standart</option>
          <option value="medium">Medium</option>
          <option value="important">Important</option>
        </select>
      </div>
    </div>

    <label>Description</label>
    <textarea v-model="note.descr"></textarea>

    <button class="btn btnPrimary btn-note" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      require: true
    }
  },
  data: () => ({
    selected: 'standart'
  }),
  methods: {
    addNote() {
      this.$emit('addNewNote', this.note);
    }
  },
}
</script>

<style lang="scss">
  .new-note {
    text-align: center;
  }

  .btn-note {
    margin: 20px 0;
  }
  .note-block {
    width: 48%;
    select {
      width: 100%;
      padding: 16px 26px;
      margin-bottom: 30px;
      border-radius: 20px;
    }
  }
</style>