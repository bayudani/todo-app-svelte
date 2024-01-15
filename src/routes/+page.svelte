<svelte:head>
    <title>todo app</title>
		<link rel="stylesheet" href="/bulma.min.css">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous" referrerpolicy="no-referrer" />

</svelte:head>

<script>

import CardList from './CardList.svelte'

    // menggunakan array untuk menampilkan data
    // let cards =[
    //     'belajar html',
    //     'belajar js',
    //     'belajar svelte',
    //     'belajar progaming',
    //     'belajar progaming1',
    //     'belajar progaming2',
    // ]


    // let taskCardsLocalStorage=JSON.parse(localStorage.getItem('Takscards'))

    // let taskCardsLocalStorage = JSON.parse(localStorage.getItem('Takscards')); // Gunakan array kosong default jika tidak ditemukan
let Taskscards = [];

    let inProgressCards =[]
    let doneCards =[]

    


    // event handler dan reactivity
    // untuk inputan
    // let todo = ""
    // // untuk memasukkan inoutan
    // function handleCard(){

    //     // cara pertaama
    //     // cards.push ({todo: 'Belajar css',list:'Task' })
    //     // cards = cards

    //     // cara kedua
    //     // cards= [...cards, {todo: 'Belajar css',list:'Task' }]


    //     // cara input dan memasukkan
    //     cards= [...cards, {todo ,list:'Task' }]
    //     todo =''

    // }

   

    function handleEventAddCard(event){
 
        let data = event.detail
        if(data.listName == 'Tasks'){
            Taskscards = [...Taskscards,{todo: data.todo}]
            localStorage.setItem('Takscards',JSON.stringify(Taskscards))
        }else if(data.listName == 'In progress'){
            inProgressCards = [...inProgressCards,{todo: data.todo}]

        }else {
            doneCards = [...doneCards,{todo: data.todo}]

        }
    }

    function hanldeEventDeleteCard(event){
        let data = event.detail

        if(data.listName == 'Tasks'){

            Taskscards.splice(data.index,1)
            Taskscards = Taskscards
        }else if (data.listName == 'In progress'){
            inProgressCards.splice (data.index,1)
            inProgressCards = inProgressCards
        }else{
            doneCards.splice(data.index,1)
            doneCards=doneCards
        }
    }

    function handleEventMoveRight(event){
        let data = event.detail

        if (data.listName == 'Tasks'){
            let cardToMove =Taskscards.splice(data.index,1)
            inProgressCards = [...inProgressCards,cardToMove[0]]
            Taskscards=Taskscards
        }else if (data.listName == 'In progress'){
            let cardToMove =inProgressCards.splice(data.index,1)
            doneCards = [...doneCards,cardToMove[0]]
            inProgressCards=inProgressCards
        }
    }

    function handleEventMoveleft(event){
        let data = event.detail

        if (data.listName =='In progress'){
            let cardToMovel = inProgressCards.splice(data.index,1)
            Taskscards = [...Taskscards,cardToMovel[0]]
            inProgressCards=inProgressCards
        }else if(data.listName == 'Done'){
        let cardToMovel = doneCards.splice(data.index,1)
            inProgressCards = [...inProgressCards,cardToMovel[0]]
            doneCards=doneCards
        }

    }
</script>


<div class="container is-fluid">
    <h1 class="is-size-3">Todo App</h1>
    <div class="columns">
     <CardList 
     cards={Taskscards} 
     listName={'Tasks'} 
     on:addCard={handleEventAddCard} 
     on:deleteCard={hanldeEventDeleteCard}
     on:moveRight={handleEventMoveRight}>
    </CardList>

     <CardList 
     cards={inProgressCards}
     listName={'In progress'} 
     on:addCard={handleEventAddCard}
     on:deleteCard={hanldeEventDeleteCard}
     on:moveRight={handleEventMoveRight}
     on:moveLeft={handleEventMoveleft}>
    </CardList>

     <CardList 
     cards={doneCards} 
     listName={'Done'}
      on:addCard={handleEventAddCard}
      on:deleteCard={hanldeEventDeleteCard}
      on:moveLeft={handleEventMoveleft}>
    </CardList>
    </div>
</div>

<!-- <style>
    h1{
        color: tomato;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }
</style> -->