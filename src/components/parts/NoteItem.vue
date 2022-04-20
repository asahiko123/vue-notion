<template>
  <div class="note-family"
    @mouseover="onMouseOver"
    @mouseleave="onMouseLeave"
    v-bind:class="{mouseover: note.mouseover && !note.editing}"
  >
    <template v-if="note.editing">
      <input v-model="note.name" class="transparent" @keypress.enter="onEditEnd" />
    </template>
    <template v-else>
    <div class="note-icon" @click="onClickChildNote(note)">
      <i class="fas fa-file-alt"></i>
    </div>
    <div class="note-name">{{note.name}}</div>

    <div v-show="note.mouseover" class="buttons">
      <div class="button-icon">
        <i class="fas fa-sitemap"></i>
      </div>
      <div class="button-icon">
        <i class="fas fa-plus-circle"></i>
      </div>
      <div class="button-icon" @click="onClickEdit(note)">
        <i class="fas fa-edit"></i>
      </div>
      <div class="button-icon" @click="onClickDelete(note)">
        <i class="fas fa-trash"></i>
      </div>
    </div>
    </template>
    <div class="child-note">
      <NoteItem 
        v-for="childNote in note.children"
        v-bind:key="childNote.id"
        v-bind:note="childNote"
        @delete="onClickDelete"
        @editStart="onEditNoteStart"
        @editEnd="onEditNoteEnd"
        @addChild="onAddChildNote"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NoteItem',
  props: [
    'note',
  ],
  methods: {
    onMouseOver : function() {
      return this.note.mouseover = true;
    },
    onMouseLeave : function() {
      return this.note.mouseover = false;
    },
    onClickDelete : function(note) {
      this.$emit('delete', note);
    },
    onClickEdit : function(note) {
      this.$emit('editStart', note);
    },
    onEditEnd : function() {
      this.$emit('editEnd');
    },
    onClickChildNote: function(note){
      this.$emit('addChild',note);
    }
  },
}
</script>

<style scoped lang="scss">
.note {
  margin: 10px 0;
  display: flex;
  align-items: center;
  padding: 5px;
  color: rgba(25, 23, 17, 0.6);
  &.mouseover {
    background-color: rgb(232, 231, 228);
    cursor: pointer;
  }
  .note-icon {
    margin-left: 10px;
  }
  .note-name {
    width: 100%;
    padding: 3px 10px;
  }
  .buttons {
    display: flex;
    flex-direction: row;
    .button-icon {
      padding: 3px;
      margin-left: 3px;
      border-radius: 5px;
    }
  }
}
</style>