<template>
    <v-app id="inspire">

        <v-app-bar app clipped-left>
            <v-toolbar-title class="green--text">NoteTaker</v-toolbar-title>
        </v-app-bar>

        <v-content>
 
            <div class="" style="width: 500px; margin: auto;">
                <div>
                    
                    <v-tabs color="green" v-model="tab" vertical>
                        <v-tab v-for="item in items" :key="item.tab">
                            {{item.tab}}
                        </v-tab>
                        <v-tabs-items v-model="tab">
                            <v-tab-item v-for="item in items" :key="item.tab">
                                <v-card flat>
                                    <v-card-text>
                                        <v-text-field v-show="tab!=0" label="Requested ID" single-line v-model="item_id">
                                        </v-text-field>
                                        <v-text-field v-show="tab==0 || tab==3" label="Name" single-line v-model="name">
                                        </v-text-field>
                                        <span v-show="isSuccess">The operation was a success.</span>
                                        <span v-show="!isSuccess">The operation failed.</span>
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
                <v-card
                    dark
                    max-width="344"
                    class="mx-auto v-card"
                    v-show="output!=null"
                    v-for="(row, index) in output"
                    :key="index"
                >
                    <v-card-title>
                        {{row.name}}
                    </v-card-title>
                    <v-card-text>
                        ID: {{row.item_id}}
                    </v-card-text>
                </v-card>
            </div>

        </v-content>

        <v-footer app>
            <span>&copy; 2019 - Layout Components from Vuetify</span>
        </v-footer>
    </v-app>
</template>

<script>

    export default {
        props: {
            source: String,
        },
        data: () => ({

            tab: null,
            name: null,
            item_id: null,
            output: null,
            isSuccess: false,

            items: [
                { tab: 'INSERT', content: 'Insert a name for the field' },
                { tab: 'GET', content: 'Insert a name for the field' },
                { tab: 'DELETE', content: 'Insert a name for the field' },
                { tab: 'UPDATE', content: 'Insert a name for the field'},
            ],
         }),
        methods: {
            makeReq: function () {
                const url = 'https://5261puzqsb.execute-api.us-west-2.amazonaws.com/default';
                //const key = 'szqaVuropf37NRM8CgdhH3ekEynhYaEewYYz36Qb';

                var reqdata = {};

                reqdata["action"] = this.items[this.tab].tab;

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

                const params = {
                    method: "POST",
                    body: JSON.stringify(reqdata)
                };
             
                fetch(url, params)
                    .then(data => {
                        return data.json();
                    })
                    .then(res => {
                        console.log(res);
                        if (res.affectedRows && res.affectedRows > 0) {
                            this.output = null;
                            this.isSuccess = true;
                        }
                        else {
                            this.output = res;
                            this.isSuccess = false;
                        }
                    })

                    .catch(error => this.output = error)
                    this.item_id = null;
            }
        }
    }
</script>

<style scoped>
    .selectWrap {
        display: flex;
        justify-content: center;     
        margin: auto;
    }
    .btn {
        margin: 10px;
    }
    .tbl {
        text-align: center;
        margin: auto;
        padding: 10px;
        /* border: 5px soild red; */
    }
    .tbl th, .tbl td {
        padding: 10px 20px;
    }
    .names {
        text-align: left;
    }
    .v-card {
        margin: 20px;
    }
</style>