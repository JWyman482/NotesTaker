<template>
    <div>
        <v-tabs color="green" v-model="tab" vertical>
            <v-tab v-for="(item, index) in items" :key="index">
                {{item}}
            </v-tab>
            <v-tabs-items v-model="tab">
                <v-tab-item v-for="item in items" :key="item">
                    <v-card flat>
                    <v-card-text>
                        <v-text-field v-show="tab!=0" label="Requested ID" single-line v-model="item_id"/>
                        <v-text-field v-show="tab==0 || tab==3" label="Name" single-line v-model="name"/>

                    </v-card-text>
                    <v-card-actions>
                        <v-btn class="btn" color="green" small dark @click="makeReq">
                        Submit
                        </v-btn>
                    </v-card-actions>
                    </v-card>
                </v-tab-item>
            </v-tabs-items>
        </v-tabs>
    </div>
</template>

<script>
export default {
    data: () => ({
        items: [
            'INSERT',
            'GET',
            'DELETE',
            'UPDATE'
        ],
        tab: null,
        name: null,
        item_id: null,
    }),
    methods: {
        makeReq() {
                 
                var reqdata = {};
                
                console.log("Inside makeReq.");
                console.log(this.items[0]);

                reqdata["action"] = this.items[this.tab];
                console.log("Inside makeReq in NoteInput");

                // INSERT
                if (this.tab == 0) {
                    reqdata["name"] = this.name;
                }

                // GET
                if (this.tab == 1 && this.item_id != null) {
                    reqdata["id"] = "id";
                    reqdata["item_id"] = this.item_id;
                }

                // DELETE
                if (this.tab == 2 && this.item_id != null) {
                    reqdata["item_id"] = this.item_id;
                }

                // UPDATE
                if (this.tab == 3 && this.item_id != null) {
                    reqdata["item_id"] = this.item_id;
                    reqdata["name"] = this.name;
                }
                // reqdata["name"] = this.name;
                // reqdata["id"] = this.itemid;
                console.log(reqdata);

                this.$emit('makeReq', reqdata);
        }
    }
}

</script>

<style scoped>

</style>