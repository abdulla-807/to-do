<template>
  <div>
    <Navbar></Navbar>
    <Notes :notes="notes"/>
    <Modal v-show="modalOpen" @closeModal="closeModal"/>
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
        modalOpen: false
      }
    },
    methods: {
      openModal(){
        this.modalOpen = true
      },
      closeModal(){
        this.modalOpen = false
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>