<template>
    <div>
        <Message :show.sync="msgShow" :type="msgType" :msg="msg" />
    </div>
</template>

<script>
export default {
    name: 'Home',
    data() {
        return {
            msg: '', // 消息
            msgType: '', // 消息类型
            msgShow: false // 是否显示消息, 默认不显示
        }
    },
    // 组件内的路由导航守卫
    beforeRouterEnter(to, from, next) {
        const fromName = from.name// 路由的名称，对应路由配置中的 name

        next(vm => {// 确认导航
            if(vm.$store.state.auth) { // 通过 vm 参数访问组件实例，已登录时，评估路由名称
                switch (fromName) {
                    case 'Register':// 如果从注册页面跳转过来
                        vm.showMsg('注册成功')
                        break
                }
            }
        })
    },
    methods: {
        showMsg(msg, type = 'success') {
            this.msg = msg
            this.msgType = type
            this.msgShow = true
        }
    }
}
</script>

<style scoped>

</style>