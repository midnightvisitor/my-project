<template>
    <div :class="{'main-left active': vm.isMenuVisible, 'main-left': !vm.isMenuVisible}">
        <h3 class="menu-title" >
            <span v-show="!vm.isMenuVisible">
                <i class="el-icon-m-home"></i>
                工作台
            </span>
            <i class="el-icon-m-expand" @click="handleMenuToggle();"></i>
        </h3>
        <div class="main-menu">
            <!--<el-menu :default-active="activeMenu" class="main-menu-box" :collapse="vm.isMenuVisible"-->
            <el-menu :default-active="$route.path" class="main-menu-box" :collapse="vm.isMenuVisible" :unique-opened="true" text-color="#6c7993" active-text-color="#555e71">
                <sub-menu :menuList="menuList"></sub-menu>
            </el-menu>
        </div>
    </div>
</template>
<script>
    import SubMenu from './SubMenu.vue';
    import { mapState, mapActions } from 'vuex';
    export default {
        data () {
            return {};
        },
        computed: {
            ...mapState({
                menuList: state => state.main.menuList,
                // activeMenu: state => state.main.activeMenu,
                tabList: state => state.main.tabList,
                vm: state => state.main.vm
            }),

            activeMenu: {
                get () {
                    return this.$store.state.main.activeMenu;
                },
                set (val) {
                    this.$store.commit('setActiveTab', val);
                }
            }
        },
        components: {
            SubMenu
        },
        methods: {
            ...mapActions([
                'getMenu',
                'addTabMenu'
            ]),

            handleOpen (key, keyPath) {
                console.log(key, keyPath);
            },
            handleClose (key, keyPath) {
                console.log(key, keyPath);
            },

            handleMenuToggle () { // 展开收起菜单
                // this.vm.isMenuVisible = !this.vm.isMenuVisible;
                this.$store.commit('MenuToggle');
            }

        },
        created () {
            this.getMenu();
        }
    };
</script>
<style lang="less">
    @import "../../assets/css/modules/variables.less";
    .main-left {
        position: relative;
        flex-basis: 260px;
        flex-shrink: 0;
        background: @color-fff;
        transition: all ease .2s;
    }

    .main-left.active {
        flex-basis: 54px;
        overflow: hidden;
    }

    .menu-title {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 48px;
        padding: 0 20px;
        line-height: 48px;
        color: @color-000;

        i {
            font-size: 18px;
            cursor: pointer;
        }
    }

</style>
