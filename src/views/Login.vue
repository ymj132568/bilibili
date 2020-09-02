<template>
    <div>
        <login-top Text='登录'>
            <div slot="right" @click="$router.push('/register')" style="font-size:3.611vw">注册</div>
        </login-top>
        <login-text lable='账号'
        placeholder="输入账号"
        @contentWatch="res=>model.username=res"
         style="margin:4.167vw 0"
        >
        </login-text>
        <login-text lable='密码'
        placeholder="输入密码"
        @contentWatch="res=>model.password=res"
        >
        </login-text>
        <login-btn @TextClick="AjaxInsert" BtnText='登录'></login-btn>
    </div>
</template>
<script>
import LoginTop from '@/components/common/LoginTop.vue'
import LoginText from '@/components/common/LoginText.vue'
import LoginBtn from '@/components/common/LoginBtn.vue'
export default {
    data () {
        return {
            model:{}
        }
    },
    components:{
         LoginTop,
        LoginText,
        LoginBtn
    },
    methods: {
        async AjaxInsert(){
            let rulg=/^.{6,16}$/
            if(rulg.test(this.model.username)&&rulg.test(this.model.password)){
                const res=await this.$http.post('/login',this.model)
                this.$msg.fail(res.data.msg)
                if(res.data.code==301||res.data.code==302){
                    return
                }
                localStorage.setItem('token',res.data.token)
                localStorage.setItem('id',res.data.id)
                setTimeout(()=>{
                    this.$router.push('/userinfo')
                },1000)
            }else{
                this.$msg.fail("重新输入")
            }
        }
    },
}
</script>