<template>
    <div class="foot">
        Copyright © 2018 IRIS Foundation Ltd. All rights reserved.
        <a :href="'/privacy/?lang='+$store.state.lang">Privacy</a>
        &
        <a :href="'/terms?lang='+$store.state.lang">Terms</a>
    </div>
</template>

<script>
    export default {
        name: "foot"
    }
</script>

<style scoped lang='less'>
    .foot {
        a {
            color: #3DA0FF ;
        }
        z-index: 10;
        position: fixed;
        bottom: 0;
        height: 40px;
        width: 100%;
        background: #2D2948;
        line-height: 40px;
        color: #8c8fa6 ;
        font-size: 14px;
        text-align: center;
    }
</style>