<script>
    import {onMount} from 'svelte';
    import { goto } from '$app/navigation';
    
    import { page } from '$app/stores';

    let active = "is-active"

    //Tab active effect
    let specsTab = "is-active"
    let dimenTab = ""
    let capTab = ""
    let mecTab = ""
    let safeTab = ""

    //Car info
    let id = ""
    let variantId = ""

    let carBrand = ""
    let carName = ""

    //Details
    let variantName = ""
    let price = 0

    //Specifications
    let engine = 0
    let engineType = ""
    let fuel = ""
    let power = ""
    let torque = ""
    let mileage = 0
    let drivetrain = ""
    let Transmission = ""

    //dimensions
    let length = 0
    let width = 0
    let height = 0
    let weight = 0

    //capacity
    let doors = 0
    let seating = 0
    let rows = 0
    let boot = 0
    let tank = 0

    //mechanicals
    let frontBrake = ""
    let backBrake = ""
    let steering = ""
    let wheels = ""
    let frontWheels = ""
    let rearWheels = ""

    //safety
    let airbags = 0
    let safetyRating = ""

    onMount(async () => {
        
        id = $page.url.searchParams.get('car') || ""
        variantId = $page.url.searchParams.get('variant') || ""
        fetchVariant()
        
    })

    function changeTab(tab){

        switch(tab){
            case 0:
                specsTab = "is-active"
                dimenTab = ""
                capTab = ""
                mecTab = ""
                safeTab = ""
                break
            case 1:
                specsTab = ""
                dimenTab = "is-active"
                capTab = ""
                mecTab = ""
                safeTab = ""
                break
            case 2:
                specsTab = ""
                dimenTab = ""
                capTab = "is-active"
                mecTab = ""
                safeTab = ""
                break
            case 3:
                specsTab = ""
                dimenTab = ""
                capTab = ""
                mecTab = "is-active"
                safeTab = ""
                break
            case 4:
                specsTab = ""
                dimenTab = ""
                capTab = ""
                mecTab = ""
                safeTab = "is-active"
                break
        }

    }

    //Get car specific variant from api
    async function fetchVariant(){

        active = "is-active"

        const response = await fetch(`https://us-central1-autowiz-1001.cloudfunctions.net/app/api/cars/getCar/${id}`, {
          method: "GET",
          headers: {'Content-Type': 'application/json'}
        })

        let content = await response.json();

        let car = content
        carBrand = car.brand
        carName = car.name

        let variants = car.variants

        let variant = variants[variantId]

        //Details
        variantName = variant.variant
        price = variant.price

        //Specifications
        engine = variant.Specifications.engine
        engineType = variant.Specifications.engineType
        fuel = variant.Specifications.fuel
        power = variant.Specifications.power
        torque = variant.Specifications.torque
        mileage = variant.Specifications.mileage
        drivetrain = variant.Specifications.drivetrain
        Transmission = variant.Specifications.Transmission

        //dimensions
        length = variant.dimensions.length
        width = variant.dimensions.width
        height = variant.dimensions.height
        weight = variant.dimensions.weight

        //capacity
        doors = variant.capacity.doors
        seating = variant.capacity.seating
        rows = variant.capacity.rows
        boot = variant.capacity.boot
        tank = variant.capacity.tank

        //mechanicals
        frontBrake = variant.mechanicals.frontBrake
        backBrake = variant.mechanicals.backBrake
        steering = variant.mechanicals.steering
        wheels = variant.mechanicals.wheels
        frontWheels = variant.mechanicals.frontWheels
        rearWheels = variant.mechanicals.rearWheels

        //safety
        airbags = variant.safety.airbags
        safetyRating = variant.safety.safetyRating

        active = ""

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
                                <div class="is-size-1 has-text-centered"><span class="has-text-weight-normal">{carBrand} {carName}</span> <span class="has-text-weight-semibold">{variantName}</span></div>
                                <div class="is-size-3 has-text-centered is-italic">
                                    <span>${price}</span>
                                </div>
                                <div class="tabs is-centered is-toggle is-medium is-hidden-mobile">
                                    <!-- svelte-ignore a11y-missing-attribute -->
                                    <!-- svelte-ignore a11y-click-events-have-key-events -->
                                    <ul>
                                      <li class="{specsTab}">
                                        <a on:click={() => changeTab(0)}>
                                          <span>Specifications</span>
                                        </a>
                                      </li>
                                      <li class="{dimenTab}">
                                        <a on:click={() => changeTab(1)}>
                                          <span>Dimensions</span>
                                        </a>
                                      </li>
                                      <li class="{capTab}">
                                        <a on:click={() => changeTab(2)}>
                                          <span>Capacity</span>
                                        </a>
                                      </li>
                                      <li class="{mecTab}">
                                        <a on:click={() => changeTab(3)}>
                                          <span>Mechanicals</span>
                                        </a>
                                      </li>
                                      <li class="{safeTab}">
                                        <a on:click={() => changeTab(4)}>
                                          <span>Safety</span>
                                        </a>
                                      </li>
                                    </ul>
                                  </div>
                                  <div class="menu is-hidden-desktop">
                                    <!-- svelte-ignore a11y-missing-attribute -->
                                    <!-- svelte-ignore a11y-click-events-have-key-events -->
                                    <ul class="menu-list">
                                        <li>
                                          <a on:click={() => changeTab(0)}>
                                            <span>Specifications</span>
                                          </a>
                                        </li>
                                        <li>
                                          <a on:click={() => changeTab(1)}>
                                            <span>Dimensions</span>
                                          </a>
                                        </li>
                                        <li>
                                          <a on:click={() => changeTab(2)}>
                                            <span>Capacity</span>
                                          </a>
                                        </li>
                                        <li>
                                          <a on:click={() => changeTab(3)}>
                                            <span>Mechanicals</span>
                                          </a>
                                        </li>
                                        <li>
                                          <a on:click={() => changeTab(4)}>
                                            <span>Safety</span>
                                          </a>
                                        </li>
                                      </ul>
                                  </div>
                                  <hr/>
                                {#if specsTab==="is-active"}
                                <div class="container">
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Engine</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{engine}cc</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Engine Type</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{engineType}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Fuel</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{fuel}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Power</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{power}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Torque</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{torque}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Mileage</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <!--Mileage with unit-->
                                            <div><span>{mileage}</span>{#if fuel==="EV"}<span>km</span>{:else if fuel==="CNG"}<span>kmkg</span>{:else}<span>kmpl</span>{/if}</div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Drivetrain</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{drivetrain}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Transmission</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{Transmission}</span></div>
                                        </div>
                                    </div>
                                </div>
                                {/if}
                                {#if dimenTab==="is-active"}
                                <div class="container">
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Length</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{length}mm</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Width</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{width}mm</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Height</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{height}mm</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Weight</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{weight}kg</span></div>
                                        </div>
                                    </div>
                                </div>
                                {/if}
                                {#if capTab==="is-active"}
                                <div class="container">
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Doors</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{doors}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Seating</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{seating}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Rows</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{rows}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Boot</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{boot} l</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">tank</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{tank} l</span></div>
                                        </div>
                                    </div>
                                </div>
                                {/if}
                                {#if mecTab==="is-active"}
                                <div class="container">
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Front Brake</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{frontBrake}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Back Brake</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{backBrake}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Steering</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{steering}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Wheels</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{wheels}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Front Wheels</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{frontWheels}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Rear Wheels</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{rearWheels}</span></div>
                                        </div>
                                    </div>
                                </div>
                                {/if}
                                {#if safeTab==="is-active"}
                                <div class="container">
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Airbags</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{airbags}</span></div>
                                        </div>
                                    </div>
                                    <div class="columns is-size-5 is-centered">
                                        <div class="column is-4">
                                            <div><span class="has-text-weight-semibold">Safety Rating</span></div>
                                        </div>
                                        <div class="column is-4">
                                            <div><span>{safetyRating}</span></div>
                                        </div>
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
</section>

