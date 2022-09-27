<template>
    <div class="absolute left-0 right-0 bottom-10 w-1/1 xl:w-5/6 2xl:w-7/12 mx-2 lg:mx-5 xl:mx-auto h-auto bg-gray-300 rounded-sm lg:rounded-lg px-1.5 lg:px-2 space-y-1 lg:space-y-2 py-1.5 lg:py-2">
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <div v-for="rows, index in firstrow" :key="index" class="flex">
                <Button :value="rows"/>
            </div>
            <GrowButton value="<="/>  
        </div> 
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <GrowButton value="tab" />
            <div v-for="rows, index in secondrow" :key="index" class="flex">
                <Button :value="rows" />
            </div>
        </div>
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <GrowButton value="caps" />
            <div v-for="rows, index in thirdrow" :key="index" class="flex">
                <Button :value="rows" />
            </div>
            <GrowButton value="enter" />
        </div>
        <div class="flex space-x-1 lg:space-x-2 justify-center">
            <GrowButton value="shift" />
            <div v-for="rows, index in fourthrow" :key="index" class="flex">
                <Button :value="rows" />
            </div>
            <GrowButton value="shift" />
        </div>
        <div class="flex space-x-2 justify-center">
            <GrowButton value="space" @input-text="onClickButton" @click="onClickButton" />
        </div>
    </div>
</template>

<script>
import Button from './Button.vue';
import GrowButton from './GrowButton.vue';
export default {
    components: { Button, GrowButton },
    data(){
        return{
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
        onClickButton(event) {
            this.$emit('clicked', 'someValue')
        }
    }
}
</script>

<style>

</style>