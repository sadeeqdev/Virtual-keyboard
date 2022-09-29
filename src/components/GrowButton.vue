<template>
    <div 
        @click="textClick"  
        class="relative disable-text-select grow md:h-8 lg:h-14 xl:h-16 flex justify-center items-center rounded lg:rounded-lg shadow-md bg-gray-50 hover:cursor-pointer" 
        :class="{'bg-gray-300': toggleButton, 'bg-slate-200': clickEffect}" 
        @click.right.prevent
    >
        <div class="text-gray-900 text-sm lg:text-xl">
            {{value}}
        </div>
        <div v-if="value == 'shift' && shiftValue == true || value == 'caps' && capsValue == true " class="absolute flex justify-self-end justify-end right-1 lg:right-5">
            <div class="w-1 h-1 lg:w-2 md:h-2 rounded-full bg-green-600">
            </div>
        </div>
    </div>
</template> 

<script>
export default {
    props: {
        value: String,
        keyCode: String,
        checkShift: Boolean,
        checkCaps: Boolean
    },
    data() {
        return {
            shiftValue: this.checkShift,
            capsValue: this.checkCaps,
            toggleButton: false,
            keyPressed: '',
            clickEffect: false
        }
    },
    methods: {
        textClick() {
            this.clickEffect = true
            setTimeout(() => {
                this.clickEffect = false
            }, 100)
            this.$emit('input-text', this.value)
        },
        setToggle(e) {
            let buttonCode = e.keyCode
            if (buttonCode == this.keyCode) {
                this.toggleButton = true
            }
        },
        resetToggle(e) {
            let buttonCode = e.keyCode
            if (buttonCode == this.keyCode) {
                this.toggleButton = false
            }
        }

    },
    watch: {
        checkShift: function (newVal) {
            this.shiftValue = newVal
        },
        checkCaps: function (newVal) {
            this.capsValue = newVal
        }
    },
    created() {
        window.addEventListener('keydown', this.setToggle);
        window.addEventListener('keyup', this.resetToggle);
    },
    destroyed() {
        window.removeEventListener('keydown', this.setToggle);
        window.removeEventListener('keyup', this.resetToggle);
    },

}
</script>

<style scoped>
.disable-text-select {
    user-select: none;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
}
</style>