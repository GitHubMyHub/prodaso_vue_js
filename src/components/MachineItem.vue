<template>
    <div class="machine-item">
        {{machine.name}} -> 
        <p v-if="machine.status == 1">Production</p>
        <p v-else>StandBy</p>
        <button @click="$emit('del-machine', machine.id)" class="del">x</button>
        <button @click="$emit('edit-machine', machine.id)" class="edit">E</button>
    </div>
</template>

<script>
export default {
    name: "MachineItem",
    props: ["machine"],
    methods: {

    }
}
</script>

<style scoped>
    .edit {
        background-color: green;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float:right;
    }
    .del {
        background-color: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float:right;
    }
</style>