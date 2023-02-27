<template>
    <input v-model="searchingStr" type="text" class="input" placeholder="Search...">
</template>
<script>
export default {
    data() {
        return {
            searchingStr: '',


        }
    },

    watch: {
        searchingStr(){
            this.$emit('searchingStr', this.searchingStr)
        }
    }
    
}
</script>
<style lang="scss" scoped>
    .input {
        display: flex;
        height: 55px;
        border: #EDF5E1;
        color: #EDF5E1;
        background: #1E1E1E;
        padding: 20px 24px;
        font-size: 18px;
        font-weight: 700;
        border-radius: 8px;
        align-items: center;
        cursor: pointer;
        justify-content: center;
        transition: all .1s ease-out;

        border: 2px solid #EDF5E1;
        border-radius: 12px;

        // &:hover {
        //     color: #1E1E1E;
        //     background: #EDF5E1;
        //     transition: all .2s ease-in;
        // }

    }
</style>