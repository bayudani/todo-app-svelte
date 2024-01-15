<script>
        import {createEventDispatcher} from 'svelte'
        import TodoCard from './TodoCard.svelte' //import dari file todocard

        export let cards,listName

        const dispatch = createEventDispatcher()

        let todo = ""
    // untuk memasukkan inoutan
    function handleAddCard(){

        // cara pertaama
        // cards.push ({todo: 'Belajar css',list:'Task' })
        // cards = cards

        // cara kedua
        // cards= [...cards, {todo: 'Belajar css',list:'Task' }]


        // cara input dan memasukkan
        // cards= [...cards, {todo ,list:'Task' }]

        dispatch('addCard', {todo,listName})
        todo =''
    }

    function handleDeleteCard(event){
        let data = event.detail
        dispatch('deleteCard',{index:data.index,listName})
    }

    function handleMoveRight (event){
        let data =event.detail
        dispatch('moveRight',{index:data.index,listName})
    }

    function handleMoveLeft (event){
        let data = event.detail
        dispatch ('moveLeft',{index:data.index,listName})
    }
</script>
<style></style>

<div class="column is-4">
    <div class="card has-background-light">
        <div class="card-header">
            <p class="card-header-title">{listName}</p>
        </div>
        <div class="card-content">
            <!-- mengirim data ke content yang telah di buat di todoapp -->
            <!-- <TodoCard content={'Belajar html'}/> 
            <TodoCard content={'belajar js'}/>
            <TodoCard content={'belajar svelte'}/> -->

            <!-- untuk mengambil/menampilkan data yang bersifat dinamis di ambil dari array -->
            <!-- {#each  cards as card}
            <TodoCard content={card}/> 
                
            {/each} -->

                <!-- untuk mengambil data menggunkan list array of object -->
                {#each  cards as card, index}
                <TodoCard 
                content={card.todo}
                listName={listName}
                index={index} 
                on:deleteCard={handleDeleteCard}
                on:moveRight ={handleMoveRight}
                on:moveLeft = {handleMoveLeft}
                /> 
                
            {/each}
            
            <!-- menampilkan data yang di ambil dari array yang sudah di buat -->
            <!-- <TodoCard content={cards[0]}/> 
            <TodoCard content={cards[1]}/>
            <TodoCard content={cards[2]}/> -->

            <!-- code sebelum di sederhanakan dengan membuat komponen di todo app -->
            <!-- <div class="card mb-3 has-background-primary-light">
                <div class="card-content">
                    <p class="has-text-primary-dark">belajar html</p>
                </div>
            </div>
            <div class="card mb-3 has-background-primary-light">
                <div class="card-content">
                    <p class="has-text-primary-dark">belajar js</p>
                </div>
            </div>
            <div class="card mb-3 has-background-primary-light">
                <div class="card-content">
                    <p class="has-text-primary-dark">belajar sevlet</p>
                </div>
            </div> -->


            <!-- reactivity svelte(perubah pada langsung pada svelte disini kita membuat nya) 

            //menambah todo
            <p>{todo }</p>
            //menambah inputan ke let todo
            <input type="text" class="input is-primary" bind:value={todo}>
            <button class="button is-primary mt-1">Add To Card</button> -->

            <!-- event handlers (agar bisa memasukkan inputan ke dalam list card)-->
            <!-- <p>{todo}</p> -->
            <input type="text" class="input is-primary" bind:value={todo}>
            <button on:click={handleAddCard} class="button is-primary mt-1">Add To Card</button> 
        </div>
    </div>
</div>