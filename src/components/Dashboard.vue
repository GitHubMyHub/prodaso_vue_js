<template>
  <div id="app">
    <AddMachine v-on:add-machine="addMachine" />
    <Machines v-bind:machines="machines" v-on:edit-machine="editMachine" v-on:del-machine="deleteMachine" />
    <Modal v-bind:machine="machine" v-on:save-machine="saveMachine" v-if="showModal" @close="showModal = false" />
  </div>
</template>

<script>
import Machines from "../components/Machines";
import AddMachine from "../components/AddMachine";
import Modal from "../components/Modal";
import axios from "axios";

export default {
  name: "Dashboard",
  components: {
    Machines,
    AddMachine,
    Modal
  },
  data() {
    return {
      machines: [],
      showModal: false,
      machine: {}
    };
  },
  methods: {
    editMachine(id) {
      console.log("EDIT");
      
      const entry = this.machines.filter((item) => item.id === id)[0]

      console.log(entry)

      this.machine = entry

      this.showModal = true

      console.log(id);
    },
    deleteMachine(id) {
      axios
        .delete(`http://localhost:8080/machine/${id}`)
        .then(() => this.machines = this.machines.filter((machine) => machine.id !== id))
        .catch((err) => console.log(err));

      //this.machines = this.machines.filter((machine) => machine.id !== id);
    },
    addMachine(newMachine) {
      const { name, status } = newMachine;

      axios
        .post("http://localhost:8080/addMachine", {
          name,
          status,
        })
        .then((res) => (this.machines = [...this.machines, res.data]))
        .catch((err) => console.log(err));
    },
    saveMachine(){
      console.log("SaveMachine")

      const {id, name, status} = this.machine

      axios.put(`http://localhost:8080/machine/${id}`, {name, status}).then().catch(err => console.log(err))

      console.log(this.machine)
      this.showModal = false
    }
  },
  created() {
    axios
      .get("http://localhost:8080/machines")
      .then((res) => (this.machines = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
/* MODAL */
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
