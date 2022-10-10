<template>
  <div>
    <div v-if="modalShow">
      <modal
       :modalType="modalType"
       :form-item="selectedRow"
       @closeModal="closeModal"
       
       @saveData="DatahasSave"
      />
   </div>
    
    <b-container>
        <br>
        <b-button
          variant="primary"
          @click="openModal"
          @saveData="saveList()"
        >
          add more
        </b-button>
        <b-dropdown text="action" variant="dark">
            <b-dropdown-item v-b-modal.modal @click="edit">
              Edit
            </b-dropdown-item>
            <b-dropdown-item @click="deleteRow">
              Delete
            </b-dropdown-item>
        </b-dropdown>
        <br><br>

        <b-table
        id="custom-table"
        :items="items"
        :fields="fields"
        striped
        small
        primary-key="a"
        @row-selected="onRowSelected"
        selectable
        hover
        select-mode="single"
        selected-variant="primary"
      ></b-table>
    </b-container>
    

  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  components: {
    Modal: () => import('./components/Modal.vue')
  },
  data(){
    return {
        modalShow:false,
        modalType: 0,
        selectedRow: [],
        fields: [
          { key: 'id', sortable: true },
          { key: 'name', sortable: true },
          { key: 'gender', sortable: true },
        ],
        items: [
          { id: 2, name: 'Two', gender: 'Male', },
          { id: 1, name: 'Three', gender: 'Female', },
          { id: 3, name: 'Four', gender: 'Female', },
          { id: 4, name: 'One', gender: 'Male', }
        ],
       
    }
  },
  mounted(){
    // this.$root.$on('saveData', (res) => {
    //   this.items.push({
    //     id: res.id,
    //     name: res.name,
    //     gender: res[0].gender
    //   })
    // })
  },
  methods: {
    DatahasSave(res){
      this.items.push({
         id: res.id,
         name: res.name,
         gender: res[0].gender
       })     
        this.modalType = 0
        this.modalShow = false
    },
    openModal(){ 
      console.log(this.modalType ,  this.modalShow  )
      this.modalType = 1
      this.modalShow = true
      console.log(this.modalType ,  this.modalShow  )
    },
    onRowSelected(items){
      this.selectedRow = items
    },
    edit(){

      this.modalType = 2 
      this.modalShow = true
    },
    deleteRow(items){
      console.log(items[index])
    },
    closeModal(data) {
      this.modalType = 0
      this.modalShow = false
      if (data) {
        console.log(data)
        //this.setInput(data)
      }
   
    },
  }
}
</script>
