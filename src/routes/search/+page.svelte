<script>
    import { goto } from '$app/navigation';
    import {onMount} from 'svelte'

    let active = "is-active"

    //Filter details
    let size = ""
    let body = ""
    let transmission = ""
    let fuel = ""
    let preference = ""

    //Page
    let sizePage = true
    let bodyPage = false
    let transmissionPage = false
    let fuelPage = false
    let preferencePage = false

    let cars = []

    onMount(
        () => setTimeout(() => {
			active = ""
		},2000)
    )

    //Set car size
    function setSizeSmall(){
        size = "Small-Size"
        active = "is-active"
        sizePage = false
        setTimeout(() => {
			    active = ""
          bodyPage = true
		    },1000)
    }
    function setSizeMedium(){
        size = "Mid-Size"
        active = "is-active"
        sizePage = false
        setTimeout(() => {
			    active = ""
          bodyPage = true
		    },1000)
    }
    function setSizeFull(){
        size = "Full-Size"
        active = "is-active"
        sizePage = false
        setTimeout(() => {
			    active = ""
          bodyPage = true
		    },1000)
    }

    //Set car body type
    function setBodyHatch(){
      body = "Hatch"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }

    function setBodyCSedan(){
      body = "CSedan"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }
    
    function setBodyCross(){
      body = "Cross"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }

    function setBodySedan(){
      body = "Sedan"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }

    function setBodyCoupe(){
      body = "Coupe"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }
    
    function setBodySUV(){
      body = "SUV"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }
    
    function setBodyMPV(){
      body = "MPV"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }
    
    function setBodyTruck(){
      body = "Truck"
      active = "is-active"
      bodyPage = false
      setTimeout(() => {
			  active = ""
        transmissionPage = true
		  },1000)
    }
    
    //Set transmission type
    function setTransmissionAuto(){
      transmission = "Automatic"
      active = "is-active"
      transmissionPage = false
      setTimeout(() => {
			  active = ""
        fuelPage = true
		  },1000)
    }

    function setTransmissionManual(){
      transmission = "Manual"
      active = "is-active"
      transmissionPage = false
      setTimeout(() => {
			  active = ""
        fuelPage = true
		  },1000)
    }

    function setTransmissionClutchless(){
      transmission = "Clutchless"
      active = "is-active"
      transmissionPage = false
      setTimeout(() => {
			  active = ""
        fuelPage = true
		  },1000)
    }
    
    //Set fuel type
    function setFuelDiesel(){
      fuel = "Diesel"
      active = "is-active"
      fuelPage = false
      setTimeout(() => {
			  active = ""
        preferencePage = true
		  },1000)
    }

    function setFuelPetrol(){
      fuel = "Petrol"
      active = "is-active"
      fuelPage = false
      setTimeout(() => {
			  active = ""
        preferencePage = true
		  },1000)
    }

    function setFuelHybrid(){
      fuel = "Hybrid"
      active = "is-active"
      fuelPage = false
      setTimeout(() => {
			  active = ""
        preferencePage = true
		  },1000)
    }

    function setFuelEV(){
      fuel = "EV"
      active = "is-active"
      fuelPage = false
      setTimeout(() => {
			  active = ""
        preferencePage = true
		  },1000)
    }

    function setFuelCNG(){
      fuel = "CNG"
      active = "is-active"
      fuelPage = false
      setTimeout(() => {
			  active = ""
        preferencePage = true
		  },1000)
    }
    
    //Set preference type
    async function setPreferenceComfort(){
      preference = "Confort"
      const url = `/cars?size=${size}&body=${body}&transmission=${transmission}&fuel=${fuel}&preference=${preference}`
      await goto(url)
    }

    async function setPreferenceBalanced(){
      preference = "Balanced"
      const url = `/cars?size=${size}&body=${body}&transmission=${transmission}&fuel=${fuel}&preference=${preference}`
      await goto(url)
    }

    async function setPreferencePerformance(){
      preference = "Performance"
      const url = `/cars?size=${size}&body=${body}&transmission=${transmission}&fuel=${fuel}&preference=${preference}`
      await goto(url)
    }

</script>

<!--Loading-->
<div class="pageloader accent-bg {active}"></div>

{#if sizePage}
<section class="page-wrap hero is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">
          <div class="column">
            <div class="container">
                <div class="panel search-body">
                    <p class="panel-heading search-header">
                      Choose prefered car size
                    </p>
                    <div class="m-5">
                        <div class="columns">
                            <div class="column is-4">
                                <!-- svelte-ignore a11y-click-events-have-key-events -->
                                <div on:click={setSizeSmall} class="button-card card">
                                    <div class="card-image">
                                      <figure class="image p-3">
                                        <img src="../icons/size/small.png" alt="Small Car">
                                      </figure>
                                    </div>
                                    <div class="card-content">
                                      <div class="media">
                                        <div class="media-content">
                                          <p class="title is-4">Small-Size</p>
                                          <p class="subtitle is-7">Compact car for daily use</p>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                            </div>
                            <div class="column is-4">
                                <!-- svelte-ignore a11y-click-events-have-key-events -->
                                <div on:click={setSizeMedium} class="button-card card">
                                    <div class="card-image">
                                      <figure class="image p-3">
                                        <img src="./icons/size/mid.png" alt="Medium Car">
                                      </figure>
                                    </div>
                                    <div class="card-content">
                                      <div class="media">
                                        <div class="media-content">
                                          <p class="title is-4">Mid-Size</p>
                                          <p class="subtitle is-7">Big car for multipurpose</p>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                            </div>
                            <div class="column is-4">
                                <!-- svelte-ignore a11y-click-events-have-key-events -->
                                <div on:click={setSizeFull} class="button-card card">
                                    <div class="card-image">
                                      <figure class="image p-3">
                                        <img src="./icons/size/full.png" alt="Big Car">
                                      </figure>
                                    </div>
                                    <div class="card-content">
                                      <div class="media">
                                        <div class="media-content">
                                          <p class="title is-4">Full-Size</p>
                                          <p class="subtitle is-7">Huge car for highways and occasions</p>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
{/if}

{#if bodyPage}
<section class="page-wrap hero is-fullheight">
  <div class="hero-body">
    <div class="container">
      <div class="columns is-centered">
        <div class="column">
          <div class="container">
              <div class="panel search-body">
                  <p class="panel-heading search-header">
                    Choose prefered car body type
                  </p>
                  <div class="m-5">
                      <div class="columns is-centered is-multiline">
                        {#if (size==="Small-Size")}
                          <div class="column is-3">
                              <!-- svelte-ignore a11y-click-events-have-key-events -->
                              <div on:click={setBodyHatch} class="button-card card">
                                  <div class="card-image">
                                    <figure class="image p-5">
                                      <img src="../icons/body/hatch.png" alt="Hatchback">
                                    </figure>
                                  </div>
                                  <div class="card-content">
                                    <div class="media">
                                      <div class="media-content">
                                        <p class="title is-4">Hatchback</p>
                                      </div>
                                    </div>
                                  </div>
                                </div>
                          </div>
                        {/if}
                        {#if (size==="Small-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodyCSedan} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/csedan.png" alt="Compact Sedan">
                                  </figure>
                                </div>
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">C-Sedan</p>
                                    </div>
                                  </div>
                                </div>
                            </div>
                          </div>
                        {/if}
                        {#if (size==="Mid-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodyCross} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/cross.png" alt="Crossover">
                                  </figure>
                                </div>
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">Crossover</p>
                                    </div>
                                  </div>
                                </div>
                            </div>
                          </div>
                        {/if}
                        {#if (size==="Mid-Size" || size==="Full-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodySedan} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/sedan.png" alt="Sedan">
                                  </figure>
                                </div>
                                <div class="card-content is-3">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">Sedan</p>
                                    </div>
                                  </div>
                                </div>
                            </div>
                          </div>
                        {/if}
                        {#if (size==="Mid-Size" || size==="Full-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodyCoupe} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/coupe.png" alt="Coupe">
                                  </figure>
                                </div>
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">Coupe</p>
                                    </div>
                                  </div>
                                </div>
                            </div>
                          </div>
                        {/if}
                        {#if (size==="Mid-Size" || size==="Full-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodySUV} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/suv.png" alt="SUV">
                                  </figure>
                                </div>
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">SUV</p>
                                    </div>
                                  </div>
                                </div>
                            </div>
                          </div>
                        {/if}
                        {#if (size==="Mid-Size" || size==="Full-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodyMPV} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/mpv.png" alt="MPV">
                                  </figure>
                                </div>
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">MPV</p>
                                    </div>
                                  </div>
                                </div>
                            </div>
                          </div>
                        {/if}
                        {#if (size==="Mid-Size" || size==="Full-Size")}
                          <div class="column is-3">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setBodyTruck} class="button-card card">
                                <div class="card-image">
                                  <figure class="image p-5">
                                    <img src="../icons/body/truck.png" alt="Truck">
                                  </figure>
                                </div>
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">Truck</p>
                                    </div>
                                  </div>
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
  </div>
</section>
{/if}

{#if transmissionPage}
<section class="page-wrap hero is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">
          <div class="column">
            <div class="container">
                <div class="panel search-body">
                    <p class="panel-heading search-header">
                      Choose transmission type
                    </p>
                    <div class="m-5">
                        <div class="columns is-centered">
                            <div class="column is-4">
                                <!-- svelte-ignore a11y-click-events-have-key-events -->
                                <div on:click={setTransmissionAuto} class="button-card card">
                                    <div class="card-image">
                                      <figure class="image p-3">
                                        <img src="../icons/transmission/auto.png" alt="Automatic">
                                      </figure>
                                    </div>
                                    <div class="card-content">
                                      <div class="media">
                                        <div class="media-content">
                                          <p class="title is-4">Automatic</p>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                            </div>
                            
                            <div class="column is-4">
                                  <!-- svelte-ignore a11y-click-events-have-key-events -->
                                  <div on:click={setTransmissionManual} class="button-card card">
                                      <div class="card-image">
                                        <figure class="image p-3">
                                          <img src="../icons/transmission/manual.png" alt="Manual">
                                        </figure>
                                      </div>
                                      <div class="card-content">
                                        <div class="media">
                                          <div class="media-content">
                                            <p class="title is-4">Manual</p>
                                          </div>
                                        </div>
                                      </div>
                                  </div>
                            </div>
                            {#if (size!=="Full-Size")}
                            <div class="column is-4">
                                    <!-- svelte-ignore a11y-click-events-have-key-events -->
                                    <div on:click={setTransmissionClutchless} class="button-card card">
                                        <div class="card-image">
                                          <figure class="image p-3">
                                            <img src="../icons/transmission/clutchless.png" alt="Clutchless Manual">
                                          </figure>
                                        </div>
                                        <div class="card-content">
                                          <div class="media">
                                            <div class="media-content">
                                              <p class="title is-4">Clutchless Manual</p>
                                            </div>
                                          </div>
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
    </div>
  </section>
{/if}

{#if fuelPage}
<section class="page-wrap hero is-fullheight">
  <div class="hero-body">
    <div class="container">
      <div class="columns is-centered">
        <div class="column">
          <div class="container">
              <div class="panel search-body">
                  <p class="panel-heading search-header">
                    Choose prefered car body type
                  </p>
                  <div class="m-5">
                      <div class="columns is-multiline">
                          <div class="column">
                              <!-- svelte-ignore a11y-click-events-have-key-events -->
                              <div on:click={setFuelDiesel} class="button-card card">
                                  <div class="card-content">
                                    <div class="media">
                                      <div class="media-content">
                                        <p class="title is-4">Diesel</p>
                                      </div>
                                    </div>
                                  </div>
                                </div>
                          </div>
                          <div class="column">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setFuelPetrol} class="button-card card">
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">Petrol</p>
                                    </div>
                                  </div>
                                </div>
                              </div>
                          </div>
                          <div class="column">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setFuelHybrid} class="button-card card">
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">Hybrid</p>
                                    </div>
                                  </div>
                                </div>
                              </div>
                          </div>
                          <div class="column">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setFuelEV} class="button-card card">
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">EV</p>
                                    </div>
                                  </div>
                                </div>
                              </div>
                          </div>
                          {#if (size!=="Full-Size")}
                          <div class="column">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <div on:click={setFuelCNG} class="button-card card">
                                <div class="card-content">
                                  <div class="media">
                                    <div class="media-content">
                                      <p class="title is-4">CNG</p>
                                    </div>
                                  </div>
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
  </div>
</section>
{/if}

{#if preferencePage}
<section class="page-wrap hero is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">
          <div class="column">
            <div class="container">
                <div class="panel search-body">
                    <p class="panel-heading search-header">
                      Choose drive preference
                    </p>
                    <div class="m-5">
                        <div class="columns">
                            <div class="column is-4">
                                <!-- svelte-ignore a11y-click-events-have-key-events -->
                                <div on:click={setPreferenceComfort} class="button-card card">
                                    <div class="card-image">
                                      <figure class="image p-3">
                                        <img src="../icons/preference/comfort.png" alt="Comfort">
                                      </figure>
                                    </div>
                                    <div class="card-content">
                                      <div class="media">
                                        <div class="media-content">
                                          <p class="title is-4">Comfort</p>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                            </div>
                            
                            <div class="column is-4">
                                  <!-- svelte-ignore a11y-click-events-have-key-events -->
                                  <div on:click={setPreferenceBalanced} class="button-card card">
                                      <div class="card-image">
                                        <figure class="image p-3">
                                          <img src="../icons/preference/balanced.png" alt="Balanced">
                                        </figure>
                                      </div>
                                      <div class="card-content">
                                        <div class="media">
                                          <div class="media-content">
                                            <p class="title is-4">Balanced</p>
                                          </div>
                                        </div>
                                      </div>
                                  </div>
                            </div>
                            <div class="column is-4">
                                    <!-- svelte-ignore a11y-click-events-have-key-events -->
                                    <div on:click={setPreferencePerformance} class="button-card card">
                                        <div class="card-image">
                                          <figure class="image p-3">
                                            <img src="../icons/preference/performance.png" alt="Performance">
                                          </figure>
                                        </div>
                                        <div class="card-content">
                                          <div class="media">
                                            <div class="media-content">
                                              <p class="title is-4">Performance</p>
                                            </div>
                                          </div>
                                        </div>
                                    </div>
                              </div>
                        </div>
                    </div>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
{/if}

