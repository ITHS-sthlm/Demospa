<script setup>
    import HeroImage from '../components/HeroImage.vue';
</script>
<template>
    <HeroImage />
    <div id="wrapping">
        <!-- En kolumn (col) med flexbox för att centrera innehållet -->
        <div class="col" v-if="spaOffer">
            <!-- En kort (card) med bredd på 18 rem, som innehåller bild och text -->
            <div class="card" style="width: 18rem">
                <!-- En bild i kortet från sökvägen till bilden -->
                <img
                    src="../assets/img/laura-chouette-bD4j1V52dx0-unsplash.jpg"
                    class="card-img-top"
                    alt="..."
                />
                <!-- En kortkropp (card-body) med rubrik, inkluderade tjänster, pris och knapp -->
                <div class="card-body">
                    <!-- En rubrik (card-title) som visar namnet på erbjudandet -->
                    <h5 class="card-title">{{ spaOffer.name }}</h5>

                    <!-- En paragraf (p) som visar inkluderade tjänster för erbjudandet -->
                    <p>{{ spaOffer.including }}</p>

                    <!-- En paragraf som visar priset och använder dynamisk färg (grön) -->
                    <p>
                        <span :style="{ color: 'green' }"
                            >{{ spaOffer.price }} kr</span
                        >
                    </p>

                    <!-- En länk (a) som leder till sidan /spa/about och har en primär knappstil -->
                    <a href="#" class="btn btn-primary">Köp Paketet</a>
                </div>
            </div>
        </div>
        <div v-else>Loading...</div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data(){
        return {
            spaOffer: null
        }
    },
    mounted(){
        const spaId = this.$route.params.id;

        axios
        .get('/spa.json')
        .then((response) => {
            //Filtrera spa.json efter det specifika id´t
            this.spaOffer = response.data.find(
                (offer) => offer.id === spaId
            )
        })
        .catch((error)=> {
            console.error('Jaså minsann, det fungerar inte...', error)
        })
    }
}

</script>

<style scoped>
    #wrapping {
        margin-top: 10vh;
        margin-bottom: 10vh;
    }
</style>
