<template>
    <div class="comment">
        <p class="comment-title"> 
            <span>评论</span>
            <span>({{dataLength}})</span>
        </p>
        <div class="commentMyinfor">
            <img :src="myuser.user_img" alt="" v-if="myuser">
            <img src="@/assets/default_img.jpg" alt="" v-else>
            <input type="text" ref="Postipt" placeholder="输入内容" v-model="comcontent">
            <button @click="comentPublish">发表</button>
        </div>
    </div>
</template>
<script>
export default {
    props:['dataLength'],
    data () {
        return {
            myuser:null,
            comcontent:'',
        }
    },
    methods: {
        async myUserinfo(){
            const res = await this.$http.get("/user/" + localStorage.getItem("id"));
            this.myuser = res.data[0];
        },
        comentPublish(){
            if(!this.myuser&&!localStorage.getItem('token')&&localStorage.getItem('id')){
                this.$msg.fail("先登录")
                return
            }
            this.$emit('Postcomment',this.comcontent)
            this.comcontent=''
        },
        focusIpt(){
     this.$refs.Postipt.focus()
    }
    },
    created() {
        if(localStorage.getItem('token')){
            this.myUserinfo();
        }
  },
}
</script>