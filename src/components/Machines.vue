<template>
    <div>
        <div v-bind:key="machine.id" v-for="machine in machines">
            <MachineItem v-bind:machine="machine" v-on:edit-machine="$emit('edit-machine', machine.id) " v-on:del-machine="$emit('del-machine', machine.id)"/>
        </div>

    </div>

</template>

<script>
import MachineItem from "./MachineItem"
export default {
    name: "Machines",
    components: {
        MachineItem
    },
    props: ["machines"]
}
</script>

<style scoped>

</style>