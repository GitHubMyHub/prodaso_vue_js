<template>
  <div>
    <form @submit="addMachine">
      <input type="text" v-model="name" name="name" placeholder="Add Machine" />
      <select v-model="status" name="status">
          <option value="1">Production</option>
          <option value="2">StandBy</option>
      </select>
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>

export default {
  name: "AddMachine",
  data() {
    return {
      name: "",
      status: 1
    };
  },
  methods: {
    addMachine(e) {
      e.preventDefault();

      const newMachine = {
        name: this.name,
        status: this.status,
      };

      // Send up to parent
      this.$emit("add-machine", newMachine);

      this.name = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
</style>