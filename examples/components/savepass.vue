<template>
  <div>


    <mt-card title="Save Pass">
      <div class="row">
        <!--<div class="col-sm-6">
         <mt-card title="Form" minTitle="">
          <textarea class="mt-textarea" rows="10" cols="60"></textarea>
          <mt-button bg="bluegray">Submit</mt-button>
        </mt-card>
        </div> -->
        <div class="col-sm-6">
         <mt-card title="Form" minTitle="">
          <mt-input placeholder="Domain" inputSize="large" isFlag></mt-input>
          <mt-input placeholder="Username" inputSize="large" isFlag></mt-input>
          <mt-input placeholder="Password" inputSize="large" isFlag></mt-input>
          <component v-for="item in items" ref="itemRefs" :is="item" :key="item.name"></component>

          <mt-button bg="bluegray">Submit</mt-button>
          <mt-button @click="addComponent">Add Field</mt-button>
          <mt-button @click="addLabel">Add Label</mt-button>

        </mt-card>
        </div>
        
        
      </div>
    </mt-card>
    <mt-dialog title="Add Label" v-model="add_label">
      
      <div class="row">
          <div class="col-sm-8">
            <mt-input placeholder="Label" inputSize="large" v-model="labelNameToInsert" isFlag></mt-input>
          </div>
          <div class="col-sm-4">
            <mt-button class="insert_label_btn" @click="insertLabel">Add New</mt-button>
          </div>
      </div>
       <div class="row">
          <table>
    <tbody>
      <tr v-for="val in presentLabels" class="mt-table">
        <td>
          <mt-checkbox class="m-r-20" v-model="val.checked">{{val.value}}</mt-checkbox>
        </td>
      </tr>
    </tbody>
  </table>
      </div>
    </mt-dialog>

    
  </div>
</template>

<script>
import ReusableInput from './reusableInput.vue'
export default {
    data() {
      return {
        presentLabels : [{"checked" : false,"value":"Bank"},{"checked" : false,"value":"Email"},{"checked" : false,"value":"Social Network"},{"checked" : false,"value":"Other"}],
        items: [],
        add_label : false,
        labelNameToInsert : ''

      }
  },
  
  methods: {
    insertLabel(){
      const newLabel = {"checked" : false,"value": ""+this.labelNameToInsert};
      this.presentLabels.push(newLabel);  
    },
    addLabel(){
      this.add_label = true;
    },
    addComponent () {
      const renderComponent = {
        render (h) {         
          return h(ReusableInput, {
            class: ['foo'],
            
            props: { 
              name: 'Foo'
            }
          })
        }
      }
      
      this.items.push(renderComponent)      
    }
  }
};
</script>

<style scoped>
.insert_label_btn {
  margin-top: 10px;
}
</style>