<template>
    <div class="position-relative">
     
      <section style="margin-top:-10px;padding-top:10px;height: 70px; z-index: 100;
       top:0px;
      width:100%;">
        <div v-show="slider" class="container-fluid position-fixed menu-scroll" style="top: 80px;z-index: 2;margin-top: -10px;
         background-color:rgba(226, 226, 226, 0.521); margin-left: -15px; height: 70px;padding-left: 15px;">
            <div :class="[display,scroll,width]">
                <b-button variant="outline-primary" class="m-5">Primary</b-button>
                <b-button variant="outline-primary" class="m-5">Secondary</b-button>
                <b-button variant="primary" class="m-5">Success</b-button>
                <b-button variant="outline-primary" class="m-5">Danger</b-button>
                <b-button variant="outline-primary" class="m-5">Warning</b-button>
                <b-button variant="outline-primary" class="m-5">Info</b-button>
                <b-button variant="outline-primary" class="m-5">Light</b-button>
                <b-button variant="outline-primary" class="m-5">Dark</b-button>
            </div>
        </div>
        <div class="container-fluid position-fixed" :style="{'top':top,'z-index':'2','left':'50%','transform': 'translate(-50%,0)'}" v-show="iconSlideUp">
            <div class="d-flex justify-content-center">
                <div v-b-toggle.collapse-1 @click="iconSlideUp=false,toggle()" class="glyph simple-icon-options text-primary"></div>
            </div>
        </div>
      </section>
      <div>
            <div class="position-fixed" style="z-index:1;left:0px;top:70px;width: 100%;background-color: rgba(226, 226, 226, 0.521);">
                <b-collapse id="collapse-1" >
                            <b-card style="height: 1000px;background-color: rgba(226, 226, 226, 0.521);">
                               
                            </b-card>
                            <div class="container-fluid position-fixed" style="bottom: 30px;left:50%;transform: translate(-50%,0);" >
                                <div class="d-flex justify-content-center">
                                    <div v-b-toggle.collapse-1 @click="slider=true,iconSlideUp=true,slideUp()" class="glyph simple-icon-options sm text-primary"></div>
                                </div>
                            </div>
                </b-collapse>
            </div>
        
        </div>
      <!-- Element to collapse -->
          <b-collapse id="collapse-2">
                  <div style="height:89vh;width: 100%;z-index: 1 !important; position: fixed;top: 70px;
                  background-color:rgba(226, 226, 226, 0.808)" class="pl-0 pr-0"></div>
          </b-collapse>
    
        <b-row class="px-2 main">
                <b-col @click="pre_order(index)" cols="6" xs="6" lg="4" v-for="(item,index) in item" :key="index" class="pl-2 pr-2 mb-2">
                    <b-card class="mb-2 shadow" no-body>
                        <div class="position-relative">
                           <img src="https://dummyimage.com/200x160" class="card-img-top" />
                           <b-badge v-if="item.click!=0" size="sm" variant="primary" class="position-absolute rounded" style="top:10px;right:10px">
                              {{item.click}}
                          </b-badge>
                        </div>
                        <b-card-body>
                          <h6 class="mb-2 card-subtitle font-sm">Coca Cola</h6>
                          <p class="card-text text-small mb-0 font-weight-light font-xs float-left">$1.2</p>
                          <div v-b-modal.modal-center class="glyph simple-icon-options-vertical float-right"></div>
                        </b-card-body>
                    </b-card>
                </b-col>
        </b-row>
  
  
        <!-- @popup -->
        <div>
          <b-modal id="modal-center" centered class="">
              <b-row class="mb-1 position-absolute" style="top:-40px;left:54%;transform: translate(-50%,0);">
                  <b-col cols="12 d-flex justify-content-center">
                      <b class="font-md">Qty</b>
                  </b-col>
              </b-row>
              <b-row>
                  <b-col cols="12" class="qty">
                      <div class="margin-top-10 mb-1 d-flex justify-content-between ">
                          <b-form-spinbutton block class="rounded w-100 h-50 qty" id="sb-inline" v-model="value" inline>
                          </b-form-spinbutton>
                      </div>
                  </b-col>
              </b-row>
              <b-row>
                  <b-col clos="12" label="Note">
                      Note
                      <b-form-textarea
                          id="textarea-no-resize"
                          rows="3"
                          no-resize
                          class="qty"
                      ></b-form-textarea>
                  </b-col>
              </b-row>
              <template #modal-footer>
                  <div class="w-100">
                      <b-button 
                          block
                          variant="primary"
                          size="sm"
                          class="float-right rounded-default"
                          @click="show=false"
                      >
                          SAVE
                      </b-button>
                  </div>
              </template>
          </b-modal>
        </div>
       
      
    </div>
  </template>
  <script>

  export default {
    data(){
      return{
          iconSlideUp:true,
          slider: true,
          toggleValue: true,
          value: 1,
          top: "120px",
          open:false,
          qty: 0,
          test:[
              0,3,4,1,4,2,4,4,6,7
          ],
          display: "d-flex",
          scroll: "overflow-x",
          width: "w-100",
          item: [
              {
                  click:0,
                  id:1
              },
              {
                  click:2,
                  id:2
              },
              {
                  click:1,
                  id:3
              },
              {
                  click:0,
                  id:2
              },
              {
                  click:0,
                  id:3
              },
              {
                  click:0,
                  id:3
              },
              {
                  click:0,
                  id:3
              },
              {
                  click:3,
                  id:3
              },
              {
                  click:0,
                  id:3
              },
              {
                  click:0,
                  id:3
              }
  
  
          ]
      }
    },
 
    methods:{
      pre_order(index1){
          this.item.forEach((element, index) => {
              if(index1 == index){
                  element.click++;
              }
          })
      },
      toggle(){
              this.display = "d-block",
              this.padding = "10px",
              this.top = "86.5vh"
      },
      slideUp(){
              this.display = "d-flex"
              this.padding = "80px"
              this.top = "120px"
      }
    }
  }
  </script>
  <style>
    .togglebutton{
        padding : 1em;
        background-color:#2196F3;
        color:#FFF;
        cursor:pointer;
    }
    .element {
        padding : 1em;
        background-color:#B3E5FC;
        position:absolute;
        width:100%;
    }
  
  </style>