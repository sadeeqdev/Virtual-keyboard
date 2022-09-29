<template>
    <div class="absolute left-0 right-0 bottom-0 lg:bottom-10 w-1/1 xl:w-5/6 2xl:w-7/12 mx-0 lg:mx-5 xl:mx-auto h-auto bg-gray-200 rounded-sm lg:rounded-lg p-1 lg:px-2 space-y-1 lg:space-y-2 py-1.5 lg:py-2" @click.right.prevent>
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <div v-for="rows, index in firstrow" :key="index" class="flex">
                <Button :value="rows"  @input-text="onClickButton" :checkShift="shiftValue" :checkCaps="false"/>
            </div>
            <div class="hidden md:flex grow">
                <GrowButton value="backspace" keyCode="8" @input-text="onClickButton"/>
            </div>
            <div class="flex md:hidden grow">
                <GrowButton value="back" keyCode="8" @input-text="onClickButton"/>
            </div>
        </div> 
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <GrowButton value="tab"  keyCode="9" @input-text="onClickButton"/>
            <div v-for="rows, index in secondrow" :key="index" class="flex">
                <Button :value="rows"  @input-text="onClickButton" :checkShift="shiftValue" :checkCaps="capsValue"/>
            </div>
        </div>
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <GrowButton value="caps" keyCode="20" @input-text="onClickButton" :checkCaps="capsValue"/>
            <div v-for="rows, index in thirdrow" :key="index" class="flex">
                <Button :value="rows"  @input-text="onClickButton" :checkShift="shiftValue" :checkCaps="capsValue"/>
            </div>
            <GrowButton value="enter" keyCode="13" @input-text="onClickButton"/>
        </div>
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <GrowButton value="shift" keyCode="16" @input-text="onClickButton" :checkShift="shiftValue" />
            <div v-for="rows, index in fourthrow" :key="index" class="flex">
                <Button :value="rows"  @input-text="onClickButton" :checkShift="shiftValue" :checkCaps="capsValue"/>
            </div>
            <GrowButton value="shift" keyCode="16" @input-text="onClickButton" :checkShift="shiftValue"/>
        </div>
        <div class="flex space-x-2 justify-center" >
            <GrowButton value="space" keyCode="32" @input-text="onClickButton"/>
        </div>
        
    </div>
</template>

<script>
import Button from './Button.vue';
import GrowButton from './GrowButton.vue';
export default {
    components: { Button, GrowButton },
    props: {
        keyboardValue: String
    },
    data(){
        return{
            shiftValue: false,
            capsValue: false,
            textArray: [],
            textOutput: '',
            firstrow: [
                { lowercase: '`', uppercase: '~' },
                { lowercase: '1', uppercase: '!' },
                { lowercase: '2', uppercase: '@' },
                { lowercase: '3', uppercase: '#' },
                { lowercase: '4', uppercase: '$' },
                { lowercase: '5', uppercase: '%' },
                { lowercase: '6', uppercase: '^' },
                { lowercase: '7', uppercase: '&' },
                { lowercase: '8', uppercase: '*' },
                { lowercase: '9', uppercase: '(' },
                { lowercase: '0', uppercase: ')' },
                { lowercase: '-', uppercase: '_' },
                { lowercase: '=', uppercase: '+' },

            ],
            secondrow: [
                { lowercase: 'q', uppercase: 'Q' },
                { lowercase: 'w', uppercase: 'W' },
                { lowercase: 'e', uppercase: 'E' },
                { lowercase: 'r', uppercase: 'R' },
                { lowercase: 't', uppercase: 'T' },
                { lowercase: 'y', uppercase: 'Y' },
                { lowercase: 'u', uppercase: 'U' },
                { lowercase: 'i', uppercase: 'I' },
                { lowercase: 'o', uppercase: 'O' },
                { lowercase: 'p', uppercase: 'P' },
                { lowercase: '[', uppercase: '{' },
                { lowercase: ']', uppercase: '}' },
                { lowercase: "\\", uppercase: '|' }
            ],
            thirdrow: [
                { lowercase: 'a', uppercase: 'A' },
                { lowercase: 's', uppercase: 'S'},
                { lowercase: 'd', uppercase: 'D'},
                { lowercase: 'f', uppercase: 'F'},
                { lowercase: 'g', uppercase: 'G'},
                { lowercase: 'h', uppercase: 'H'},
                { lowercase: 'j', uppercase: 'J'},
                { lowercase: 'k', uppercase: 'K'},
                { lowercase: 'l', uppercase: 'L'},
                { lowercase: ';', uppercase: ':'},
                { lowercase: '\'', uppercase: '"'},
               
            ],
            fourthrow: [
                { lowercase: 'z', uppercase: 'Z' },
                { lowercase: 'x', uppercase: 'X'},
                { lowercase: 'c', uppercase: 'C'},
                { lowercase: 'v', uppercase: 'V'},
                { lowercase: 'b', uppercase: 'B'},
                { lowercase: 'n', uppercase: 'N'},
                { lowercase: 'm', uppercase: 'M'},
                { lowercase: ',', uppercase: '<'},
                { lowercase: '.', uppercase: '>'},
                { lowercase: '/', uppercase: '?'},
            ]
        }
    },
    methods: {
        onClickButton(value) {
            if(value == 'shift'){
                this.capsValue = !this.capsValue
                this.shiftValue = !this.shiftValue
            }else if (value == 'caps') {
                this.capsValue = !this.capsValue
            } else if (value == "backspace") {
                this.textArray.pop()
                this.textOutput = this.textArray.join('')
            } else if (value == "enter") {
                this.textArray.push('\r\n')
                this.textOutput = this.textArray.join('')
            } else if (value == "tab") {
                this.textArray.push('      ')
                this.textOutput = this.textArray.join('')
            } else if (value == "space") {
                this.textArray.push(' ')
                this.textOutput = this.textArray.join('')
            }else {
                this.textArray.push(value)
                this.textOutput = this.textArray.join('')
            }
            this.$emit('clicked-keyboard', this.textOutput)
        },
        removeChar(e){
            if (e.keyCode == 8){
                this.textArray.pop()
                this.textOutput = this.textArray.join('')
                this.$emit('clicked-keyboard', this.textOutput)
            }

        }
    },
    watch: {
        keyboardValue: function (newVal) {
            this.textArray = newVal.split('')
            this.textOutput = this.textArray.join('')
            this.$emit('clicked-keyboard', this.textOutput)
        }
    },

    created() {
        window.addEventListener('keydown', this.removeChar);
    },
    destroyed() {
        window.removeEventListener('keydown', this.removeChar);

    },
}
</script>
