<template>
    <div>
        <NoteInput @makeReq="request"/>
        <NoteOutput isSuccess output/>
    </div>
</template>

<script>
import NoteInput from "./NoteInput.vue"
import NoteOutput from "./NoteOutput.vue"

export default {
    components: {
        NoteOutput,
        NoteInput
    },
    data: () => ({
        output: null,
        isSuccess: false
    }),
    methods: {
        request: (reqObj) => {
                const url = 'https://5261puzqsb.execute-api.us-west-2.amazonaws.com/default';

                const params = {
                    method: "POST",
                    body: JSON.stringify(reqObj)
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

</style>