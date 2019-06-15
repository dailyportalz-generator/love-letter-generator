<template>
    <div id="sex_choice">
        <div class="button">
        <button @click="handleWomen">女の子用</button>
        <button @click="handleMen">男の子用</button>
        </div>
    </div>
</template>
<script>
    export default {
        methods:{
            handleWomen:function () {
                this.$emit('selectSex','women')
            },

            handleMen:function () {
                this.$emit('selectSex','men')
            }
        }
    }
</script>

<style scoped>
    #sex_choice{
        max-width: 800px;
        margin: 0 auto;
    }
    #sex_choice .button{
        text-align: center;
    }
</style>