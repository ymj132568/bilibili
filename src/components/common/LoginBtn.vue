<template>
    <div class="btnBox">
        <div class="btn" @click="TextClick">
            {{BtnText}}
        </div>
    </div>
</template>
<script>
export default {
    props:['BtnText'],
    methods: {
        TextClick(){
            this.$emit('TextClick')
        }
    },
}
</script>