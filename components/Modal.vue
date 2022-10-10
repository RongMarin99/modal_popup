<template>
    <div>
        <b-modal
            v-model="modal"
            scrollable
            centered
            no-close-on-backdrop
            no-close-on-esc
            hide-header-close
            title="Popup Modal Testing">
          <div>
              <b-form>
                <div v-show="false"></div>
                <div v-if="false"></div>

                     <b-input
                     v-model="list.id"
                     placeholder="id"
                     ></b-input>
                
                    <b-input v-model="list.name" placeholder="name"></b-input>
              
                    <b-form-select 
                       v-model="list[0].gender"
                       label="choose one option"
                    >
                        <option
                            v-for="(item,index) in list[0].options"
                            :value="item.value"
                            :key="index"
                        >
                        {{ item.value }}
                        </option>
                    </b-form-select>
                    <textarea v-model="address">

                    </textarea>
              </b-form>
          </div>
          <template slot='modal-footer'>
            <b-button size='xs' variant='outline-secondary' @click='clearForm'
            >Cancel
            </b-button>
            <b-button v-if="modalType==1" size='xs' variant='primary' @click='save'>Save</b-button>
            <b-button v-else-if="modalType==2" size='xs' variant='success' @click='update'>SaveChange</b-button>
          </template>
        </b-modal>
    </div>
</template>
<script>
    export default{
        props:{
            formItem: {
      type: Object,
      default: () => {
        return {}
      }
    },
            modalType: {
                type: Number,
                default: 0
             },
        },
        data(){
            return {
                modal: false,
                list: [
                    { 
                     id: '',
                     name: '',
                     gender: 'Male',
                     options: [
                         {value: "Male", enum: 1},
                         {value: "Female", enum: 2}
                        ]
                    }
                ],
                address: null
            }
        },
        watch: {
            modalType: {
            handler(val) {
                if (val == 1) {
                    this.modal = true
                } else if (val == 2) {
                    this.modal = true
                    this.list.id = this.formItem[0].id
                    console.log(this.formItem)
                //this.setData()
                }
            },
                immediate: true
            },
            address: {
            handler(new_val, old_val) {
                if(new_val != undefined){
                    if(new_val.length == 10){
                    alert('error')
                }
                }
                console.log('old' + old_val)
                console.log('new' +new_val)
            },
                immediate: true, // for component parent 
                //deep: true   // for string array
            }
        },
        methods:{
            save(){
                this.$emit('saveData', this.list)
                this.modal = false
            },
            clearForm(){
                this.modal = false
                this.list.id = null
                this.list.name = ""
                this.list.gender = "Male"

                this.$emit('closeModal', [1,2,3])
            }
        },
    }
</script>

