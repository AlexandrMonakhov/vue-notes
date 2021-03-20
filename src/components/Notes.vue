<template>

  <div class="notes">

    <div class="note" 
      v-for="(note, index) in notes" 
      :class="{ full: !grid, medium: note.type === 'medium', important: note.type === 'important' }" 
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
        <p>{{ note.title }}</p>
        <p style="cursor: pointer;" @click="removeNote(index)">&times;</p>
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
  props: {
    notes: {
      type: Array,
      require: true
    },
    grid: {
      type: Boolean,
      require: true
    }
  },
  methods: {
    removeNote(index) {
      this.$emit('removeNote', index);
    }
  }
}
</script>

<style lang="scss">
.notes { 
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}

.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #fff;
  transition: all .25s cubic-bezier(.02, .01, .47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, .02);
  border: 5px solid rgb(255, 255, 255);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, .04);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }
  &.full {
    width: 100%;
    text-align: center;
  }
  &.medium {
    border: 5px solid rgba(255, 230, 1, .50);
    &:hover {
      border: 5px solid rgba(255, 230, 1, .04);
    }
  }
  &.important {
    border: 5px solid rgba(255, 0, 0, 0.5);
    &:hover {
      border: 5px solid rgba(255, 0, 0, .04);
    }
  }
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  h1 {
    font-size: 32px;
  }
  p {
    font-size: 22px;
    color: rgb(6, 6, 155);
  }
  svg {
    color: #999;
    cursor: pointer;
    &.active {
      color: rgb(6, 6, 155);
    }
  }
  svg:not(:last-child) {
    margin-right: 12px;
  }
  &.full {
    justify-content: center;
    p:not(:last-child) {
      margin-right: 16px;
    }
  }
}

.note-body {
  p {
    margin: 20px 0;
  }
  span {
    font-size: 14px;
    color: #999;
  }
}
</style>