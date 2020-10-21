<template>
    <transition name="modal">
        <div class="modal-mask">
          <div class="modal-wrapper">
            <div class="modal-container">

              <div class="modal-header">
                <slot name="header">
                  Change your machine
                </slot>
              </div>

              <div class="modal-body">
                <slot name="body">
                  <p>Name: <input type="text" name="name" v-model="machine.name"></p>
                  <p>Status: <select name="status" v-model="machine.status">
                      <option value="1">Production</option>
                      <option value="2">StandBy</option>
                  </select></p>
                </slot>
              </div>

              <div class="modal-footer">
                <slot name="footer">
                  <button class="modal-default-button" @click="$emit('save-machine')">
                    OK
                  </button>
                </slot>
              </div>
            </div>
          </div>
        </div>
      </transition>
</template>

<script>
export default {
    name: "Modal",
    props: ["machine"],
    /*data() {
        return {
            name: "",
            status: 1
        }
    },*/
    methods: {
        saveMachine() {

            console.log(this.machine)

            /*const editMachine = {
                name: this.machine.name,
                status: this.machine.status,
            };*/

            // Send up to parent
            this.$emit("save-machine");

        }

    }
}
</script>

<style scoped>

</style>