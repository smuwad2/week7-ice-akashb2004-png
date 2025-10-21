<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                newItem: ''
            }
        },
        methods : {
            addItem(){
                if (this.newItem.trim() !== ''){
                    this.items.push(this.newItem)
                    this.newItem = ''
                }
            },
            removeItem(index){
                this.items.splice(index,1)
            }
        }
    }
</script>

<template>

    <h2>Wendy's roster</h2>
    <!-- TODO: Add Code here -->
    <ul>
      <li v-for="(item, index) in items" v-bind:key="item"> {{ item }} <button @click="removeItem(index)">Remove</button></li>  
    </ul> 
    <input v-model = "newItem" placeholder="Add new item" />
    <button @click= "addItem">Add</button>
   
</template>
