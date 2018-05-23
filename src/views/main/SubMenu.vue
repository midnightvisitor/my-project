<template>
    <div>
        <el-submenu :index="item.id" :key="item.id" v-for="(item) in menuList" v-if="item.second && item.second.length > 0">
            <template slot="title">
                <i :class="item.icon"></i>
                <span slot="title">{{item.name}}</span>
            </template>
            <!--<el-menu-item @click="handleTo(second);" :key="second.id" :index="second.id" v-for="second in item.second">-->
                <!--<i :class="second.icon"></i>{{second.name}}-->
            <!--</el-menu-item>-->
            <sub-menu :menuList="item.second"></sub-menu>
        </el-submenu>
        <el-menu-item @click="handleTo(item)" :key="item.id" :index="item.id" v-else>
            <i :class="item.icon"></i>
            <span slot="title">{{item.name}}</span>
        </el-menu-item>
    </div>
</template>
<script>
    export default {
        name: 'sub-menu',
        props: {
            menuList: {
                type: Array,
                default () {
                    return [];
                }
            }
        },
        data () {
            return {};
        },
        methods: {
            handleTo (item) {
                this.$router.push({
                    path: item.url,
                    title: item.name
                });
            }
        }
    };
</script>
<style lang="less">

</style>
