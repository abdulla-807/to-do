<template>
  <div>
    <Navbar 
    @getSearch="getSearch" 
    :lang="lang" 
    @changeLang="changeLang"
    ></Navbar>
    <!-- <Navbar @getSearch="search = $event"></Navbar> -->
    <Notes :notes="filterNotes" 
    @delNote="delNote"
    @changeNote="changeNote"
    :lang="lang"
    />
    <Modal @addNote="addNote" 
    :currentId="currentId" 
    v-show="modalOpen" 
    @closeModal="closeModal"
    :edit="edit"
    :editNote="editNote"
    @editedNote="editedNote"
    :lang="lang"
    />
    <AddButton @openModal="openModal"/>
  </div>
</template>

<script>
  import Navbar from '@/components/Navbar.vue';
  import Notes from '@/components/Notes.vue';
  import Modal from '@/components/Modal.vue';
  import AddButton from '@/components/Add-Button.vue';
  import langs from './lang';
  // import { vasya, petya } from "./lang";
  // console.log(langs);
  // console.log(vasya, petya);
  export default {
    components: {
      Navbar,
      Notes,
      Modal,
      AddButton
    },
    data(){
      return {
        notes: [
          {
            id: 1, 
            title: 'Vue',
            date: '07.05.2022',
            desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor'
          },
          {
            id: 2, 
            title: 'React',
            date: '07.05.2022',
            desc: 'Lorem ipsum dolor sit amet'
          },
          {
            id: 3, 
            title: 'Angular',
            date: '07.05.2022',
            desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor'
          },
        ],
        modalOpen: false,
        currentId: 1,
        edit: false,
        editNote: {},
        search: '',
        lang: 'ru',
        langWords: {}
      }
    },
    methods: {
      openModal(){
        this.modalOpen = true
      },
      closeModal(){
        this.modalOpen = false
        setTimeout(() => {
          this.edit = false
        }, 500);
        
      },
      addNote(item){
        this.notes.push(item)
        console.log(item);
      },
      delNote(id){
        let index = this.notes.findIndex( elem => elem.id == id )
        this.notes.splice(index, 1)
      },
      getNotes(){
        let localNotes = localStorage.getItem('notes');
        if (localNotes.length > 0) {
          this.notes = JSON.parse(localNotes);
          let last = this.notes.length - 1;
          this.currentId = last >= 0 ? this.notes[last].id + 1 : 1;
        }
      },
      changeNote(id){
        let value = this.notes.find((elem)=> elem.id == id);
        this.edit = this.modalOpen = true;
        this.editNote = value;
      },
      editedNote(obj){
        this.notes.forEach((elem)=>{
          if (elem.id == obj.id) {
            elem.title = obj.title;
            elem.desc = obj.desc;
            elem.date = obj.date
          }
        })
      },
      getSearch(val){
        this.search = val;
      },
      changeLang(val){
        this.lang = val;
        localStorage.setItem('lang', val);
      }
    },
    watch: {
      notes: {
        handler() {
          localStorage.setItem('notes', JSON.stringify(this.notes))
        },
        deep: true
      }
    },
    computed:{
      filterNotes(){
        const list = this.notes.filter((elem)=>{
          let result = elem.title.toLowerCase().includes(this.search.toLowerCase());
          return result;
        })
        return list;
      }
    },
    created(){
      this.getNotes();
      this.langWords = langs;
      this.lang = localStorage.getItem('lang') || 'ru'
    },
    provide: {
      words: langs
    }
  }
</script>

<style lang="scss" scoped>

</style>