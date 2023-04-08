<script>
    import {onMount} from 'svelte';
    import { goto } from '$app/navigation';
    
    import { page } from '$app/stores';

    let active = "is-active"

    //Car id
    let id = ""

    let car = {}

    //Car fuel boolean
    let isDiesel = true
    let isPetrol = false
    let isHybrid = false
    let isEV = false
    let isCNG = false

    //Car transmission boolean
    let isAutomatic = false
    let isManual = false
    let isClutchless = false

    let variants = []

    onMount(async () => {
        
        id = $page.url.searchParams.get('car') || ""
        fetchCar()
        
    })

    //Get car variants from api
    async function fetchCar(){

        active = "is-active"
        
        if(id==="") await goto("/")

        const response = await fetch(`https://us-central1-autowiz-1001.cloudfunctions.net/app/api/cars/getCar/${id}`, {
          method: "GET",
          headers: {'Content-Type': 'application/json'}
        })

        let content = await response.json();

        car = content

        isDiesel = car.fuel.isDiesel
        isPetrol = car.fuel.isPetrol
        isHybrid = car.fuel.isHybrid
        isEV = car.fuel.isEV
        isCNG = car.fuel.isCNG

        isAutomatic = car.transmission.isAutomatic
        isManual = car.transmission.isManual
        isClutchless = car.transmission.isClutchless

        variants = car.variants

        active = ""
        
    }

    async function showVariant(variantId){
        const url = `/variant?car=${id}&variant=${variantId}`
        await goto(url)
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
                  <div class="panel has-background-light">
                    <div class="card">
                        <div class="card-content">
                            <div class="content">
                              <div class="columns">
                                <div class="column is-4">
                                    <!-- svelte-ignore a11y-img-redundant-alt -->
                                    <div class="image is-fullwidth">
                                        <img src="{car.img}" alt="Image">
                                    </div>
                                </div>
                                <div class="column is-8">
                                    <div>
                                        <div><span class="has-text-weight-bold is-size-1">{car.brand}</span></div>
                                        <div></div><span class="has-text-weight-semibold is-size-2">{car.name}</span></div>
                                        <div class="mt-5"><span class="has-text-weight-semibold is-size-3">From</span></div>
                                        <div><span class="is-size-5 is-italic">${car.minPrice}</span></div>
                                        <div><span class="has-text-weight-semibold is-size-3">To</span></div>
                                        <div><span class="is-size-5 is-italic">${car.maxPrice}</span></div>
                                    </div>
                                </div>
                              </div>
                            </div>
                        </div>
                    </div>

                    <div class="card accent-bg">
                        <div class="card-content">
                            <div class="content">
                                <div class="columns is-centered is-multiline">
                                    <div class="column button-card m-4 is-3">
                                        <div><span class="has-text-weight-normal is-size-5">Price</span></div>
                                        <div><span class="has-text-weight-bold is-size-4">${car.minPrice} - ${car.maxPrice}</span></div>
                                    </div>
                                    <div class="column button-card m-4 is-3">
                                        <div><span class="has-text-weight-normal is-size-5">Preference</span></div>
                                        <div><span class="has-text-weight-bold is-size-4">{car.preference}</span></div>
                                    </div>
                                    <div class="column button-card m-4 is-3">
                                        <div><span class="has-text-weight-normal is-size-5">Body</span></div>
                                        <div><span class="has-text-weight-bold is-size-4">{car.body}</span></div>
                                    </div>
                                    <div class="column button-card m-4 is-3">
                                        <div><span class="has-text-weight-normal is-size-5">Fuel</span></div>
                                        {#if isDiesel}<div><span class="has-text-weight-bold is-size-4">Diesel</span></div>{/if}
                                        {#if isPetrol}<div><span class="has-text-weight-bold is-size-4">Petrol</span></div>{/if}
                                        {#if isHybrid}<div><span class="has-text-weight-bold is-size-4">Hybrid</span></div>{/if}
                                        {#if isEV}<div><span class="has-text-weight-bold is-size-4">EV</span></div>{/if}
                                        {#if isCNG}<div><span class="has-text-weight-bold is-size-4">CNG</span></div>{/if}
                                    </div>
                                    <div class="column button-card m-4 is-3">
                                        <div><span class="has-text-weight-normal is-size-5">Transmission</span></div>
                                        {#if isAutomatic}<div><span class="has-text-weight-bold is-size-4">Automatic</span></div>{/if}
                                        {#if isManual}<div><span class="has-text-weight-bold is-size-4">Manual</span></div>{/if}
                                        {#if isClutchless}<div><span class="has-text-weight-bold is-size-4">Clutchless</span></div>{/if}
                                    </div>
                                    <div class="column button-card m-4 is-3">
                                        <div><span class="has-text-weight-normal is-size-5">Size</span></div>
                                        <div><span class="has-text-weight-bold is-size-4">{car.size}</span></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="card mt-5">
                        <div class="card-content">
                            <div class="content">
                                <div class="columns has-text-weight-bold is-size-5 is-hidden-mobile my-0 has-text-centered">
                                    <div class="column">Versions</div>
                                    <div class="column">Price</div>
                                    <div class="column">Specs</div>
                                </div>
                                <hr/>
                                {#each variants as variant, i}
                                    <!-- svelte-ignore a11y-click-events-have-key-events -->
                                    <div on:click={() => showVariant(i)} class="columns button-card has-text-weight-normal is-size-6 has-text-centered">
                                    
                                        <div class="column is-size-4">
                                            <span>{car.brand} {car.name} <strong>{variant.variant}</strong></span>
                                        </div>
                                        <div class="column is-size-4">
                                            <span>${variant.price}</span>
                                        </div>
                                        <div class="column is-size-4">
                                            <span>{variant.Specifications.engine}cc, {variant.Specifications.fuel}, {variant.Specifications.Transmission}</span>
                                        </div>
                                    </div>
                                {/each}
                            </div>
                        </div>
                    </div>

                  </div>
                </div>
            </div>
        </div>
    </div>  
</section>