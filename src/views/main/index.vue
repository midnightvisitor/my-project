<template>
    <div class="app-container">
        <!-- 头部信息 Start -->
        <app-header></app-header>
        <!-- 头部信息 End -->

        <div class="app-content">
            <!-- 侧边菜单 Start -->
            <app-nav></app-nav>
            <!-- 侧边菜单 End -->

            <div class="main-right">
                <div class="app-tabs">
                    <el-tabs v-model="activeMenu" type="card" closable @tab-remove="removeTab" @tab-click="tabClick">
                        <el-tab-pane
                            v-for="(item) in tabList"
                            :key="item.name"
                            :label="item.title"
                            :name="item.path"
                        >
                        </el-tab-pane>
                    </el-tabs>
                </div>
                <div class="main-content">
                    <router-view></router-view>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="less" scoped>
    @import "./index.less";
</style>
<script>
    import AppHeader from './AppHeader.vue';
    import AppNav from './AppNav.vue';
    import { mapState, mapActions } from 'vuex';
    export default {
        name: 'main-content',
        data () {
            return {
                timer: null,
                dialog: {
                    visible: false,
                    title: ''
                },
                form: {
                    value1: '',
                    value2: ''
                }
            };
        },
        computed: {
            ...mapState({
                menuList: state => state.main.menuList,
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
            AppHeader,
            AppNav
        },
        methods: {
            ...mapActions([
                'getMenu',
                'addTabMenu'
            ]),

            tabClick (item, value) {
                console.log(item);
                console.log(value);
            },

            removeTab (tabName) {
                this.$store.commit('removeTabMenu', tabName);
            },

            handleOpen (key, keyPath) {
                console.log(key, keyPath);
            },
            handleClose (key, keyPath) {
                console.log(key, keyPath);
            },

            handleMenuToggle () { // 展开收起菜单
                this.vm.isMenuVisible = !this.vm.isMenuVisible;
            },
            handleTo (item) {
                this.$router.push({
                    path: item.url,
                    title: item.name
                });
            }
        },
        created () {
        },
        mounted () {
            if (!(this.$route.fullPath === '/' || this.$route.fullPath === '/main')) {
                // 添加tab
                // this.$store.commit('addTabMenu', this.$route);
                console.log('刷新页面，需要保留之前的信息。');
                this.$store.commit('setActiveTab', this.$route.path);
            } else {
                console.log('默认页面');
            }
        },
        beforeRouteUpdate (to, from, next) {
            if (to.meta.title) {
                document.title = to.meta.title;
            }
            if (this.tabList.find(tab => {
                return tab.title === to.meta.title;
            })) {
                console.log('已经存在了....');
            } else {
                this.$store.commit('addTabMenu', {title: to.meta.title, name: to.name, path: to.path});
                console.log('第一次打开过');
            }
            this.$store.commit('setActiveTab', to.path);
            next();
        }
    };
</script>
