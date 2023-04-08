<script>
    import {onMount} from 'svelte';
    import { goto } from '$app/navigation';
    
    import { page } from '$app/stores';

    let active = "is-active"

    let cars = []

    //Car Filters
    let size = ""
    let body = ""
    let transmission = ""
    let fuel = ""
    let preference = ""

    onMount(async () => {
        
        size = $page.url.searchParams.get('size') || ""
        body = $page.url.searchParams.get('body') || ""
        transmission = $page.url.searchParams.get('transmission') || ""
        fuel = $page.url.searchParams.get('fuel') || ""
        preference = $page.url.searchParams.get('preference') || ""
        fetchCars()
        
    })

    //Get cars from api
    async function fetchCars(){
        active = "is-active"
        
        if(size==="" || body==="" || transmission==="" || fuel==="" || preference==="") await goto("/")

        const response = await fetch(`https://us-central1-autowiz-1001.cloudfunctions.net/app/api/filter`, {
          method: "POST",
          headers: {'Content-Type': 'application/json'},
          body: JSON.stringify({
              size,
              body,
              transmission,
              fuel,
              preference
          })
        })

        let content = await response.json();

        content = JSON.stringify(content)


        cars = JSON.parse(content)

        active = ""

    }

    //show car info
    async function carInfo(id){
        const url = `/info?car=${id}`
        await window.open(url, "_blank")
    }

</script>

<!--Loading-->
<div class="pageloader accent-bg {active}"></div>

<section class="page-wrap hero is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">
          <div class="column">
            <div class="container">
                <div class="panel search-body py-1">
                    <div class="m-5">
                        <div class="columns is-centered is-multiline">
                            {#each cars as car}
                                <div class="column is-6">
                                    <!-- svelte-ignore a11y-click-events-have-key-events -->
                                    <div on:click={()=>carInfo(car.id)} class="button-card card">
                                        <div class="media">
                                            <!-- svelte-ignore a11y-img-redundant-alt -->
                                            <div class="media-left">
                                                <div class="image is-128x128 is-hidden-mobile">
                                                    <img src="{car.img}" alt="Image">
                                                </div>
                                                <div class="image is-64x64 is-hidden-desktop is-hidden-tablet pt-1">
                                                    
                                                    <img src="{car.img}" alt="Image">
                                                </div>
                                            </div>
                                            <div class="media-content">
                                                <div><span class="is-size-3 has-text-weight-medium">{car.brand} {car.name}</span></div>
                                                <div><span class="is-size-6 is-italic">${car.minPrice} - ${car.maxPrice}</span></div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            {/each}
                            {#if cars.length === 0}
                            <div class="column has-text-centered is-6">
                                <div class="container mb-5"><span class="is-size-1	has-text-weight-semibold light-text">No results found</span></div>
                                <div class="container mt-5">
                                    <a class="is-large is-responsive search-button" href="/search">
                                        Search Again
                                    </a>
                                </div>
                            </div>
                            {/if}
                        </div>
                    </div>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</section>