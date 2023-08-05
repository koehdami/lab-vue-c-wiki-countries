

<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-6">
                <div class="container mt-2 scroll-container overflow-scroll" >
                    <div v-for="country in countries" class="row ps-5">
                        <RouterLink :to="{path: `/list/${country.alpha3Code}`}">
                            <div :id="country.alpha2Code" class="col d-flex flex-column align-items-center border border-2 gap-2 p-5 border-grey">
                                <img :src="'https://flagpedia.net/data/flags/icon/72x54/' + country.alpha2Code.toLowerCase()  + '.png'">
                                <p class="fs-2">{{ country.name.common }}</p>
                            </div>
                        </RouterLink>
                    </div>
                </div>
            </div>
            <div class="col-6">
                <div class="container">
                    <div class="row">
                        <div class="col">
                            <RouterView></RouterView>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>



<script>
    import countries from "../../public/countries.json"
    export default {
        data(){
            return{
                countries: countries
            }
        }
    }
</script>


<style>
    .scroll-container{
        max-height: 100vh;
    }
</style>