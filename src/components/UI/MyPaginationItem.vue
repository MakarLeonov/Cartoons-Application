<template>
    <div :class="['button', {'active': page === pageNumber}]" @click="show">
        <slot class="slot"></slot>
    </div>
</template>
<script>
export default {
    props: {
        page: {
            type: Number,
        },

        pageNumber: {
            type: Number,
            default: 1
        }
    },

    methods: {
        show() {
            console.log('Page: ', this.page, ', PageNumber: ', this.pageNumber )
        }
    },
}
</script>
<style lang="scss" scoped>
    .button {
        display: flex;
        height: 55px;
        width: 55px;
        border: #EDF5E1;
        color: #EDF5E1;
        font-size: 18px;
        font-weight: 700;
        border-radius: 8px;
        align-items: center;
        cursor: pointer;
        justify-content: center;
        transition: all .1s ease-out;

        border: 2px solid #EDF5E1;
        border-radius: 12px;

        z-index: 0;

        &:hover {
            color: #1E1E1E;
            background: #EDF5E1;
            transition: all .2s ease-in;
        }

        .slot {
            z-index: 2;
        }
    }

    .active {
            color: #1E1E1E;
            background: #EDF5E1;
            transition: all .2s ease-in;
        }
</style>