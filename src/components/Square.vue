<template>
    <button class="button">
        {{this.value}}
    </button>
</template>

<script>
export default {
    name: 'Square',
    props: {
        value: String
    }
}
</script>

<style scoped>
    .button{
        width: 100px;
        height: 100px;
        font-size: 70px;
        font-weight: bold;
        background-color: #f7f7f7;
        border: 2px solid black;
    }
    
    .button:focus, .button:active{
        border: 2px solid black;
        border-radius: 0px;
    }

    .button:hover{
        
    }

</style>
