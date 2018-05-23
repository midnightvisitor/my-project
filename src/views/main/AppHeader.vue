<template>
    <div class="app-header">
        <h3 class="app-title"><strong>CIC智讯</strong>铁路标准开发平台</h3>
    </div>
</template>
<script>
    export default {
        data () {
            return {};
        }
    };
</script>
<style lang="less">
    @import "../../assets/css/modules/variables.less";
    .app-header {
        flex-basis: 60px;
        line-height: 60px;
        background: @brand-primary;
    }

    .app-title {
        padding-left: 18px;
        font-size: 22px;
        color: #e7f8ff;
    }
</style>
