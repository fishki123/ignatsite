<svelte:head>
    <title>Admin Panel Ignat Japan</title>
</svelte:head>
<script>
    function reOrderArray(){
        //for each Element inside our numbers array
        for(var i = 0; i<numbers.length; i++){

            // for each Element inisde our numbers array and i
            for(var x=0; x<numbers.length; x++){

                // if the number from the i loop is smaller then the number
                // from the x loop
                if(numbers[i] < numbers[x]){

                    // save the value i quickly.
                    var num = numbers[i];
                    // change the value i to the value x
                    numbers[i] = numbers[x];
                    // reorder the i value (stored as num here to x)
                    numbers[x] = num;
                }

            }

        }

    }
    const numbers = [];
    var number;
    function addNumbers(){
            var random = Math.floor(Math.random() * 99999999999)
            numbers.push(random)
            numbers = numbers;
            reOrderArray();
            console.log(random)
    }
    function remove(num)
    {
        for(var z=0; z<numbers.length; z++)
        {
            if(numbers[z] === num)
            {
                numbers.splice(z, 1)
                numbers = numbers;
            }
        }
    }
</script>
<div class="container invite">
    <button class="btn btn-sm btn-outline-secondary action-btn" on:click={addNumbers}>
        Сгенерировать хэш-пароль
    </button>
    <p class="invite">Хэш-пароль:</p>
    <ul class="nav navbar-nav hash">
        {#each numbers as num}
            <li>
                {num}
                <button class="btn btn-sm btn-outline-secondary action-btn" on:click={() => remove(num)}>
                Remove
            </button>
            </li>
        {/each}
    </ul>
</div>
<style>
    .hash
    {
        width: 25%;
        border: 1px solid #000;
        border-radius: 4px;
        background-color: #f7fafc;
        font-family: 'Roboto', sans-serif;
        padding: 1.25rem;
    }
    .invite
    {
        margin-top: 50px;
    }
</style>