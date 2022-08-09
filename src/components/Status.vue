<template>
    <div class="box"><fa  class="gear" icon="gear"/> <p>unfinished project</p></div>
</template>


<script>

export default {
    
    name: 'Status'
}

</script>
<style scoped>

    .box{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .gear{
        margin-right: 10px;
        animation: rotate 4s linear infinite;
    }
    @keyframes rotate {
        0%{
            transform: rotate(0deg);
        }100%{
             transform: rotate(360deg);
        }
    }


</style>