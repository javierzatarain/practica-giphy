<template>
    <div>
        <form @submit.prevent="onSubmit" class="Form">
            <input 
                class="FormInput"
                type="text"
                placeholder="Busqueda"
                v-validate="'required|min:5'"
                v-model="searchTerm"
            />
            <button
                class="FormButton"
                type="submit"
            >
            Buscar
            </button>
        </form>
    </div>
</template>

<script>

export default {
    name: 'ProductForm',
    data() {
        return {
            searchTerm:''
        }
    },
    methods: {
        onSubmit() {
           
            this.$validator.validate().then(
                valid => {
                    if(valid){
                        console.log('Envia datos');
                        this.$emit('search',this.searchTerm);
                    }

                }
            )
            
        }
    }
    
}
</script>


<style scoped>
    .Form{
        width:300px;
        margin:20px auto;
        background-color: white;
        border:none;
        padding:1rem 0;
        box-shadow: 5px 4px 4px 0 #bbb;
        

    }
    .FormInput{
        height: 15px;
        width:80%;
        border: 1px solid rgb(86,86,92);
        border-radius: 2px;
        margin-bottom:1rem;
        padding:0.5rem;
    }
    .FormButton{
        background-color: #42b983;
        color:white;
        border:none;
        width:100px;
        height:40px;
        border-radius:3px;
    }

    .FormButton:hover{
        background-color: #1b5a3e
    }


</style>
