<template>
    <div :class="['select-menu', (isActive) ? 'active' : '']" >
        <div class="select-btn" @click="isActive = !isActive">
            <span class="sBtn-text">{{ optionTitle }}</span>
            <i class="bx bx-chevron-down">
                <span class="material-symbols-outlined">keyboard_arrow_down</span>
            </i>
        </div>

        <transition name="slide-fade">
            <ul class="options">
                <li class="option"
                    v-for="(option, index) in options" :key="index"
                    @click="isActive = !isActive, optionTitle = option.title, changeOption(option.value)">
                    <i class="bx bxl-github" style="color: #171515;"></i>
                    <span class="option-text">{{ option.title }}</span>
                </li>
            </ul>        
        </transition>

        
    </div>
</template>
<script>
export default {

    props: {
        options: {
            type: Array,
        }
    },

    data() {
        return {
            isActive: false,
            optionTitle: this.options[0].title,
        }
    },

    methods: {
        changeOption(value){
            this.$emit('changeOption', value)
        }
    },
    
}
</script>

<style lang="scss" scoped>
.select-menu .select-btn{
    mit-width: 300px;
    width: 300px;
    display: flex;
    height: 55px;
    background: #fff;
    background: #EDF5E1;
    padding: 20px;
    font-size: 18px;
    font-weight: 700;
    border-radius: 8px;
    align-items: center;
    cursor: pointer;
    justify-content: space-between;
    box-shadow: 0 0 5px rgba(0,0,0,0.1);
    
    transition: all .2s ease-out;
}
.select-btn i{
    font-size: 25px;
    transition: 0.3s;
}
.select-menu.active .select-btn i{
    transform: rotate(-180deg);
}
.select-menu .options{
    position: relative;
    position: absolute;
    padding: 20px;
    margin-top: 10px;
    border-radius: 8px;
    background: #fff;
    background: #EDF5E1;
    box-shadow: 0 0 3px rgba(0,0,0,0.1);
    display: none;    
    transition: all .2s ease-out;

}
.select-menu.active .options{
    
    width: 300px;
    display: block;
}

.options .option{
    display: flex;
    height: 55px;
    cursor: pointer;
    // padding: 0 16px;
    border-radius: 8px;
    align-items: center;
    background: #fff;
    background: #EDF5E1;
    transition: all .1s ease-out;
}
.options .option:hover{
    background: #F2F2F2;
    background: #1E1E1E;
    color: #F2F2F2;
    
    transition: all .2s ease-in;
}
.option i{
    font-size: 25px;
    margin-right: 12px;
}
.option .option-text{
    font-size: 18px;
    font-weight: 600;
    // color: #333;
}

.option .option-text:hover{
    color: #F2F2F2;
    transition: all .2s ease-in;
}

.bx-chevron-down {
    display: flex;
    align-items: center;
    justify-content: center;

    span {
        font-size: 30px;
    }
}

.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>