<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                input: ''
            }
            
        },
        methods: {
            deleteItem(index){
                this.items.splice(index, 1)
            },
            addItem(){
                this.items.push(this.input)
                this.input = '';
            }
        }
    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
     
     <ul>
        <li v-for="(item, index) of items">
            {{ item }} <button @click="deleteItem(index)">Delete!</button>
        </li>
     </ul>
     <input v-model="input"/> <button @click="addItem()">Add!</button>
   
</template>