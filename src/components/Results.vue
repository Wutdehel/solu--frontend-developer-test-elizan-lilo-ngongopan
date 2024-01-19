<template>
    <div v-if="gender.probability">
        <p>{{name}} is <span :class="{'blue-text': gender.gender === 'male', 'red-text': gender.gender !== 'male'}">{{gender.gender}}</span> with a probability of {{gender.probability*100}}%</p>
    </div>
    <div v-if="gender.probability === 0">
        <p>Please input your name or use your nickname</p>
    </div>
</template>
<script>
export default {
    name: "Results",
    props: ["gender", "name"],
}
</script>
<style>
    .blue-text {
        color: #11009E;
    }   

    .red-text {
        color: #E6B9DE;
    }
</style>