<template>
    <div class="container">
        <div class="row">
            <div class="col d-flex flex-column">
                <img v-if="country" class="align-self-center pb-4" style="width:300px;" :src="'https://flagpedia.net/data/flags/icon/72x54/' + country.alpha2Code.toLowerCase()  + '.png'">
                <div class="d-flex flex-column items-align-center gap-3 fs-4 text-center">
                    <p v-if="country" class="fs-2">{{ country.name.common }}</p>
                    <div class="d-flex gap-5 border-bottom py-2">
                        <div class="w-100">Capital</div>
                        <div v-if="country" class="w-100">{{ country.capital[0] }}</div>
                    </div>
                    <div class="d-flex gap-5 border-bottom py-2">
                        <div class="w-100">Area</div>
                        <div v-if="country" class="w-100">{{ country.area }} km²</div>
                    </div>
                    <div class="d-flex gap-5 border-bottom py-2">
                        <div class="w-100">Borders</div>
                        <div class="w-100">
                            
                                <p v-if="country" v-for="item in country.borders">
                                    <RouterLink :to="{path: `/list/${item.alpha3Code}`}">
                                        {{ item.name }}
                                    </RouterLink>
                                </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>



<script>
    import { ref }  from 'vue'
    import countries from "../../public/countries.json"
    export default {
        data(){
            return{
                countries: countries,
                country: ref()
            }
        },
        methods:{
            returnCountry(searchCode){
                let countryArr = {}
                for(let item of countries){
                    if(item.alpha3Code === searchCode){
                        countryArr = item;
                    }
                }
                if(countryArr.borders){
                    for(let i = 0; i < countryArr.borders.length; i++){
                        for(let item of countries){
                            if(countryArr.borders[i] === item.alpha3Code){
                                countryArr.borders[i] = {"name": item.name.common, "alpha3Code":item.alpha3Code}
                            }
                        }
                    }
                }
                return countryArr;
            }
        },
        mounted(){
            this.country = (this.returnCountry(this.$route.params.alpha3Code))
        },
        updated(){
            this.country = (this.returnCountry(this.$route.params.alpha3Code))
        }
    }
</script>

<style></style>