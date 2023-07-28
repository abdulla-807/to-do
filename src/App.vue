<template>
  <div>
    <Navbar></Navbar>
    <Notes :notes="notes" @delNote="delNote"/>
    <Modal @addNote="addNote" :currentId="currentId" v-show="modalOpen" @closeModal="closeModal"/>
    <AddButton @openModal="openModal"/>
  </div>
</template>

<script>
  import Navbar from '@/components/Navbar.vue';
  import Notes from '@/components/Notes.vue';
  import Modal from '@/components/Modal.vue';
  import AddButton from '@/components/Add-Button.vue';
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
        currentId: 1
      }
    },
    methods: {
      openModal(){
        this.modalOpen = true
      },
      closeModal(){
        this.modalOpen = false
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
    created(){
      this.getNotes()
    }
  }
</script>

<style lang="scss" scoped>

</style>