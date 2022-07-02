<template>
    <li class="list-group-item d-flex justify-content-between w-50">
        <span :class="[item.completed ? 'completed' : '', 'item']">{{
            item.name
        }}</span>
        <button class="btn-danger ml-3" @click="removeItem()">X</button>
    </li>
</template>

<script>
export default {
    props: ["item"],
    methods: {
        removeItem() {
            axios
                .delete(`api/item/${this.item.id}`)
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios delte ", error);
                });
        }
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}
.item {
    word-break: break-all;
}
</style>
