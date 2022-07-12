<template>
  <Navbar 
    @getSearch="search = $event" 
    :lang="lang"
    @changeLang="changeLang"
  />
  <Notes
    :lang="lang"
    :notes="filterNotes"
    @delNote="delNote"
    @changeNote="changeNote"
  />
  <Modal
    :lang="lang"
    :editNote="editNote"
    :currentId="currentId"
    :edit="edit"
    @addNote="addNote"
    v-show="modalOpen"
    @close="modalOpen = $event"
    @editedNote="editedNote"
    @closeModal="closeModal"
  />
  <AddButton v-if="!search"  @openModal="openModal" />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Notes from "@/components/Notes.vue";
import Modal from "@/components/Modal.vue";
import AddButton from "@/components/AddButton.vue";
import langs from "./lang.js";



export default {
  name: "App",
  components: {
    Navbar,
    Notes,
    Modal,
    AddButton,
  },
  data() {
    return {
      currentId: 1,
      search: "",
      lang: 'ru ',
      langwords: {},
      modalOpen: false,
      edit: false,
      editNote:{},
      notes: [
        // { id: 1, title: 'Vue', descr: 'Lorem ipsum dolor sit amet', date: '07.03.2022'},
        // { id: 2, title: 'React', descr: 'Lorem ipsum dolor sit amet', date: '07.03.2022'},
        // { id: 3, title: 'Angular', descr: 'Lorem ipsum dolor sit amet', date: '07.03.2022'},
      ],
    };
  },
  created() {
    this.getNotes()
    localStorage.lang = localStorage.lang || 'ru'
    this.lang = localStorage.lang || 'ru';
    this.langwords = langs
    localStorage.words = JSON.stringify(this.langwords)
  },
  provide() {
    return {
      words: JSON.parse(localStorage.words)
    }
  },
  computed:{
      filterNotes(){
          return this.search ? this.notes.filter(item => item.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes;
      },
  },
  methods: {
    closeModal(status) {
     this.edit = this.modalOpen = status
    },
    openModal() {
      this.modalOpen = true 
      this.edit = false
    },
    addNote(item) {
      if (item.title != "" && item.descr != "") {
        this.notes.push(item);
      }
    },
    delNote(id) {
      let index = this.notes.findIndex(note => note.id == id);
      this.notes.splice(index, 1);
    },
    getNotes() {
      const localNotes = localStorage.notes
      if(localNotes) {
        this.notes = JSON.parse(localNotes)
      }
    },
    changeNote(id) {
      this.edit = this.modalOpen = true
      let pickedNote = this.notes.find(note => note.id === id)
      this.editNote = pickedNote;
    },
    editedNote(noteEdited) {
       this.notes.forEach(note => {
          if(note.id == noteEdited.id) {
            note.title = noteEdited.title;
            note.descr = noteEdited.descr;
            note.date = noteEdited.date
          }
      })
    },
    changeLang(val) {
        this.lang  = localStorage.lang = val
    } 
  },
  watch:{
    notes:{
      handler(updatedNotes) {
        // console.log(updatedNotes);
        localStorage.notes = JSON.stringify(this.notes)
      },
      deep: true
    }
  }
};
</script>

<style>
</style>