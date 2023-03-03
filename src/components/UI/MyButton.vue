<template>
    <div class="button">
        <slot></slot>
    </div>
</template>
<script>
export default {
    
}
</script>
<style lang="scss" scoped>
    .button {
        display: flex;
        height: 55px;
        border: #EDF5E1;
        color: #EDF5E1;
        padding: 20px 24px;
        font-size: 18px;
        font-weight: 700;
        border-radius: 8px;
        align-items: center;
        cursor: pointer;
        justify-content: center;
        transition: all .2s ease-out;

        border: 2px solid #EDF5E1;
        border-radius: 12px;

        &:hover {
            color: #1E1E1E;
            background: #EDF5E1;
            transition: all .25s ease-in;
        }

    }
</style>