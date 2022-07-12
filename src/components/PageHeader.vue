<template>

    <div class="logo-div">
        <h1>boolflix</h1>
    </div>

</template>

<script>

    export default {
        name: "PageHeader"
    }

</script>

<style lang="scss">

    @import "../style/colors.scss";

    .logo-div {
        padding: 20px 0;
        background-color: $secondary-color;
        h1 {
            color: $primary-color;
            text-align: center;
            text-transform: uppercase;
        }
    }

</style>