<template>
    <div>
        <form id="gender" @submit.prevent="handleSubmit">
            <input type="text" v-model="gender.name" placeholder="Enter your name"/>
            <div class="btn-container">
                <button type="submit" class="btn">Know Your Gender</button>
                <button class="btn reset" @click="handleReset">Reset</button>
            </div>
        </form>
        <div v-if="gender.submitted">
            <Results :gender="gender.data" :name="gender.submitedName"/>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import Results from "./Results.vue";

export default {
    name: "Gender",
    data() {
        return {
            gender: {
                name: "",
                data: "",
                submitedName: "",
                submitted: false,
            },
        };
    },
    methods: {
        handleSubmit() {
            const trimmedName = this.gender.name.replace(/\s/g, '');
            axios.get(`https://api.genderize.io/?name=${trimmedName}`).then((res) => {
                this.gender.data = res.data;
                this.gender.submitedName = this.gender.name
                this.gender.submitted = true;
            }).catch((err) => {
                console.log(err);
            });
        },
        handleReset() {
            this.gender.name = '';
            this.gender.submitted = false;
        },
    },
    components: { Results },
};
</script>

<style>
    form {
        display: flex;
        flex-direction: column;
    }
    .btn-container {
        display: flex;
        margin-top: 2.2rem;
        justify-content: space-evenly;
    }

    input {
        border-radius: 8px;
        border: 2px solid #030637;
        height: 2rem;
    }
</style>
