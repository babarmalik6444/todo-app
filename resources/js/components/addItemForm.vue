<template>
    <div class="mt-3">
        <h2>add item form</h2>
        <div class="container">
            <div class="row">
                <div class="col-md-4 offset-md-3">
                    <input
                        type="test"
                        placeholder="add item"
                        class="form-control w-100"
                        v-model="item.name"
                    />
                </div>
                <div class="col-md-4">
                    <button
                        :class="[item.name ? 'btn btn-primary float-left' : 'btn btn-secondary float-left']"
                        @click="addItem()"
                        >
                        add item
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        };
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }

            axios
                .post("api/item/store", {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 201) {
                        this.item.name = "";
                        this.$emit("reloadlist");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};
</script>

<style scoped></style>
