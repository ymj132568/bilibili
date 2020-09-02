<template>
    <div>
        <van-cell-group>
            <van-field
           :placeholder="placeholder" 
            :type='type'
            v-model="content"
            :lable='lable'
            />
        </van-cell-group>
    </div>
</template>
<script>
export default {
    data () {
        return {
            content:''
        }
    },
    props:['lable','placeholder','type'],
    watch: {
        content(){
            this.$emit('contentWatch',this.content)
        }
    },
}
</script>