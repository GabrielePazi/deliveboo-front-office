<script>
import axios from "axios";

import Card from '../components/Card.vue';
import SectionInfo from "../components/SectionInfo.vue";
import HeroSection from "../components/HeroSection.vue";


export default {
    components: {
        Card,
        HeroSection,
        SectionInfo,
    },
    data() {
        return {
            restaurants: [],
            selectedTypes: {
                Pizza: {
                    value: 'false',
                },
                Sushi: {
                    value: 'false',
                },
                Hamburger: {
                    value: 'false',
                },
                Poke: {
                    value: 'false',
                },
                Cinese: {
                    value: 'false',
                },
                Indiano: {
                    value: 'false',
                }
            },
            search: {
                type: '',
            },
            loading: false,
        }
    },

    methods: {
        fetchRestaurants() {
            this.loading = true;
            axios.get('http://127.0.0.1:8000/api/restaurants')
                .then((response) => {
                    this.restaurants = response.data.results;
                    //console.log(this.types)
                })
                .finally(() => {
                    this.loading = false;
                });
        },

        filterByCheckbox() {
            this.loading = true;
            // Esegui la richiesta axios con i tipi selezionati
            axios.get('http://127.0.0.1:8000/api/restaurants', { params: this.selectedTypes })
                .then((response) => {
                    this.restaurants = response.data.results;
                    this.searchError = response.data.error;
                })
                .finally(() => {
                    this.loading = false;
                });
        },
    },
    mounted() {
        this.fetchRestaurants();
    }
}
</script>


<template>
    <HeroSection></HeroSection>
    <!-- SearchBar -->
    <!-- <form @keydown.enter.prevent="filterRestaurants()" class="m-3" style="width: 200px;">
        <input class="form-control" type="search" placeholder="Search" aria-label="Search" v-model="search.type">
    </form> -->

    <div class="container my-4">
        <div class="border-arrow my-5">
            <div class="d-flex">
                <span class="bg-orange-text-white px-2">
                    RISTORANTI
                </span>
                <div class="arrow"></div>

            </div>
        </div>
        <div class="row">
            <!-- Pizza -->
            <div class="col-sm-6 col-md-4 col-lg-2">
                <label>
                    <input type="checkbox" v-model="selectedTypes.Pizza.value">
                    Pizza
                </label>
            </div>

            <!-- Sushi -->
            <div class=" col-sm-6 col-md-4 col-lg-2">
                <label>
                    <input type="checkbox" v-model="selectedTypes.Sushi.value">
                    Sushi
                </label>
            </div>

            <!-- Hamburger -->
            <div class="col-sm-6 col-md-4 col-lg-2">
                <label>
                    <input type="checkbox" v-model="selectedTypes.Hamburger.value">
                    Hamburger
                </label>
            </div>

            <!-- Poke -->
            <div class="col-sm-6 col-md-4 col-lg-2">
                <label>
                    <input type="checkbox" v-model="selectedTypes.Poke.value">
                    Poke
                </label>
            </div>

            <!-- Cinese -->
            <div class="col-sm-6 col-md-4 col-lg-2">
                <label>
                    <input type="checkbox" v-model="selectedTypes.Cinese.value">
                    Cinese
                </label>
            </div>

            <!-- Indiano -->
            <div class="col-sm-6 col-md-4 col-lg-2">
                <label>
                    <input type="checkbox" v-model="selectedTypes.Indiano.value">
                    Indiano
                </label>
            </div>
            <!-- button -->
            <div class="d-flex justify-content-center" id="locali">
                <button @click="filterByCheckbox()" class="btn btn-primary btn-sm my-3 rounded-pill custom-btn"
                    style="width: auto; max-width: 150px;">Cerca</button>
            </div>
            <!-- loader -->
            <div v-if="loading" class="loader-container mb-5">
                <svg v-if="loading" class="custom-animation-moto" xmlns="http://www.w3.org/2000/svg" width="35" height="23"
                    viewBox="0 0 95 83">
                    <g fill="none" fill-rule="evenodd">
                        <path fill="#727272" d="M25.978 73.33a6.623 6.623 0 1 1-13.227-.722 6.623 6.623 0 1 1 13.227.722" />
                        <path stroke="#565655" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M25.978 73.33a6.623 6.623 0 1 1-13.227-.722 6.623 6.623 0 1 1 13.227.722z" />
                        <path fill="#F7BE5D" d="M43.565 44.755a2.392 2.392 0 1 1-4.776-.263 2.392 2.392 0 0 1 4.776.263" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M43.565 44.755a2.392 2.392 0 1 1-4.776-.263 2.392 2.392 0 0 1 4.776.263z" />
                        <path fill="#B7B7B7"
                            d="M26.748 31.935c-.025.23-.043.464-.056.698-.407 7.463 5.312 13.844 12.776 14.251l.304-5.578a7.947 7.947 0 0 1-7.502-8.369c.013-.236.04-.467.073-.697" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M26.748 31.935c-.025.23-.043.464-.056.698-.407 7.463 5.312 13.844 12.776 14.251l.304-5.578a7.947 7.947 0 0 1-7.502-8.369c.013-.236.04-.467.073-.697" />
                        <path fill="#B7B7B7"
                            d="M29.318 48.557c.256-4.688 1.571-8.875 3.491-11.854-1.516-3.146-3.714-5.2-6.315-5.343-5.352-.292-10.107 7.079-10.62 16.464" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M29.318 48.557c.256-4.688 1.571-8.875 3.491-11.854-1.516-3.146-3.714-5.2-6.315-5.343-5.352-.292-10.107 7.079-10.62 16.464" />
                        <path fill="#E85666"
                            d="M41.282 49.33a1.566 1.566 0 0 1-1.447-1.64c.022-.416.205-.798.516-1.076a1.55 1.55 0 0 1 1.125-.396l4.48.245a1.57 1.57 0 0 1 1.47 1.641 1.55 1.55 0 0 1-.516 1.076 1.55 1.55 0 0 1-1.125.396l-4.503-.247" />
                        <path fill="#575756"
                            d="M46.006 46.07l-.03-.002-4.478-.244a1.94 1.94 0 0 0-1.41.496 1.94 1.94 0 0 0-.647 1.348 1.962 1.962 0 0 0 1.814 2.055l.03.002 4.478.245a1.956 1.956 0 0 0 2.057-1.844 1.962 1.962 0 0 0-1.814-2.056m-.055.788a1.164 1.164 0 0 1-.145 2.323l-4.478-.244-.018-.002a1.163 1.163 0 0 1 .145-2.323l4.478.245.018.001" />
                        <path fill="#FFD731"
                            d="M11.21 68.34a.396.396 0 0 1-.128-.03l-2.083-.89a.395.395 0 0 1-.197-.54l1.83-3.647a.395.395 0 0 1 .495-.19l2.222.862a.396.396 0 0 1 .205.555l-1.969 3.674a.397.397 0 0 1-.376.207" />
                        <path fill="#565655"
                            d="M11.039 62.622a.79.79 0 0 0-.76.434l-1.83 3.646a.787.787 0 0 0 .395 1.08l2.082.891a.79.79 0 0 0 1.007-.353l1.969-3.673a.79.79 0 0 0-.41-1.11l-2.222-.863a.79.79 0 0 0-.231-.052m-.055.788l2.222.863-1.969 3.674-2.082-.89 1.829-3.647" />
                        <path fill="#FDDE66" d="M53.96 48.717a2.719 2.719 0 1 1-5.43-.296 2.719 2.719 0 0 1 5.43.296" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M53.96 48.717a2.719 2.719 0 1 1-5.43-.296 2.719 2.719 0 0 1 5.43.296z" />
                        <path fill="#E85666" d="M15.244 60.391l14.018.765-.488 8.927-18.1-.988z" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M15.244 60.391l14.018.765-.488 8.927-18.1-.988z" />
                        <path fill="#E85666"
                            d="M52.332 64.185l-2.269-12.822-4.746-2.209.302 14.08-8.18 4.612-11.358-.62a2.994 2.994 0 1 0-.327 5.98l13.212.722a2.996 2.996 0 0 0 3.154-2.827 2.984 2.984 0 0 0-.56-1.912l5.984-4.566 4.788-.438z" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M52.332 64.185l-2.269-12.822-4.746-2.209.302 14.08-8.18 4.612-11.358-.62a2.994 2.994 0 1 0-.327 5.98l13.212.722a2.996 2.996 0 0 0 3.154-2.827 2.984 2.984 0 0 0-.56-1.912l5.984-4.566 4.788-.438z" />
                        <path fill="#727272"
                            d="M59.099 75.138a6.625 6.625 0 1 1-13.228-.725 6.625 6.625 0 0 1 13.228.725" />
                        <path stroke="#565655" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M59.099 75.138a6.625 6.625 0 1 1-13.228-.725 6.625 6.625 0 0 1 13.228.725z" />
                        <path fill="#FFF" d="M55.497 74.941a3.018 3.018 0 1 1-6.026-.33 3.018 3.018 0 0 1 6.026.33" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M55.497 74.941a3.018 3.018 0 1 1-6.026-.33 3.018 3.018 0 0 1 6.026.33z" />
                        <path fill="#FFF" d="M22.378 73.133a3.017 3.017 0 1 1-6.025-.328 3.017 3.017 0 0 1 6.025.328" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M22.378 73.133a3.017 3.017 0 1 1-6.025-.328 3.017 3.017 0 0 1 6.025.328z" />
                        <path fill="#E85666"
                            d="M49.032 63.262a7.65 7.65 0 0 0-4.962 9.616l14.578-4.655a7.652 7.652 0 0 0-9.616-4.96" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M49.032 63.262a7.65 7.65 0 0 0-4.962 9.616l14.578-4.655a7.652 7.652 0 0 0-9.616-4.96z" />
                        <path fill="#E85666"
                            d="M20.144 63.07c-5.434-.222-10.02 4.005-10.24 9.44l19.68.799c.22-5.434-4.005-10.019-9.44-10.24" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M20.144 63.07c-5.434-.222-10.02 4.005-10.24 9.44l19.68.799c.22-5.434-4.005-10.019-9.44-10.24z" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M15.576 69.954l5.684.31" />
                        <path fill="#F2919F"
                            d="M33.848 59.268a2.729 2.729 0 0 1-2.874 2.576l-15.15-.827a2.729 2.729 0 0 1 .296-5.449l15.152.827a2.728 2.728 0 0 1 2.576 2.873" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M33.848 59.268a2.729 2.729 0 0 1-2.874 2.576l-15.15-.827a2.729 2.729 0 0 1 .296-5.449l15.152.827a2.728 2.728 0 0 1 2.576 2.873z" />
                        <path fill="#E85666" d="M51.049 52.158l-6.344-1.516.264-4.846 6.471-.816z" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M51.049 52.158l-6.344-1.516.264-4.846 6.471-.816z" />
                        <path fill="#7DAFD3"
                            d="M37.018 55.002c.558-3.397-3.217-3.697-3.565-3.655l-4.036-.22a7.094 7.094 0 0 0-.225-2.197l-13.257-1.29a7.101 7.101 0 0 0 6.004 10.19c.353.02 1.54.084 1.803.1l6.03.328-1.006 6.829 6.279 1.382 1.973-11.467" />
                        <path stroke="#565655" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M37.018 55.002c.558-3.397-3.217-3.697-3.565-3.655l-4.036-.22a7.094 7.094 0 0 0-.225-2.197l-13.257-1.29a7.101 7.101 0 0 0 6.004 10.19c.353.02 1.54.084 1.803.1l6.03.328-1.006 6.829 6.279 1.382 1.973-11.467" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M30.792 51.202l-6.815-.372" />
                        <path fill="#FFF"
                            d="M33.408 63.206h-.014l-1.831-.1-1.53-.085a1.077 1.077 0 0 0-1.134 1.017l-.185 3.375 2.606.142v-.014l1.832.1 4.435.256a4.443 4.443 0 0 0-4.18-4.691" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M33.408 63.206h-.014l-1.831-.1-1.53-.085a1.077 1.077 0 0 0-1.134 1.017l-.185 3.375 2.606.142v-.014l1.832.1 4.435.256a4.443 4.443 0 0 0-4.18-4.691z" />
                        <path fill="#F7BE5D" d="M40.008 47.166a2.391 2.391 0 1 1-4.775-.261 2.391 2.391 0 0 1 4.775.261" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M40.008 47.166a2.391 2.391 0 1 1-4.775-.261 2.391 2.391 0 0 1 4.775.261z" />
                        <path fill="#B7B7B7"
                            d="M22.971 37.385c.6 6.58 5.948 11.898 12.74 12.268l.305-5.577a7.95 7.95 0 0 1-7.393-6.546" />
                        <path stroke="#575756" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M22.971 37.385c.6 6.58 5.948 11.898 12.74 12.268l.305-5.577a7.95 7.95 0 0 1-7.393-6.546" />
                        <path fill="#FFD731"
                            d="M17.083 58.71a2.38 2.38 0 0 1-2.57 2.174l-11-.89a2.381 2.381 0 0 1-2.174-2.572l2.294-12.256a2.38 2.38 0 0 1 2.572-2.173l7.833.656a2.38 2.38 0 0 1 2.173 2.572l.872 12.49z" />
                        <path stroke="#565655" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M17.083 58.71a2.38 2.38 0 0 1-2.57 2.174l-11-.89a2.381 2.381 0 0 1-2.174-2.572l2.294-12.256a2.38 2.38 0 0 1 2.572-2.173l7.833.656a2.38 2.38 0 0 1 2.173 2.572l.872 12.49z" />
                        <path fill="#F7C100"
                            d="M31.614 35.795c.332.19.696.328 1.084.407.176.035.355.063.539.074a3.69 3.69 0 0 0 3.785-2.813l.64-1.253-7.285-2.48a2.367 2.367 0 0 1-.974-.644l-5.073 3.978 7.284 2.731zM33.634 25.77l5.476 1.864a7.067 7.067 0 0 0-1.413-5.049l-4.063 3.185z" />
                        <path fill="#FFD731"
                            d="M34.336 20.182a7.06 7.06 0 0 0-8.938 4.453l-3.003 7.704 1.935.725 5.073-3.978a2.388 2.388 0 0 1-.523-2.4 2.398 2.398 0 0 1 3.043-1.498l1.711.582 4.063-3.185a7.017 7.017 0 0 0-3.36-2.403" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M28.88 26.686a2.398 2.398 0 0 1 3.043-1.498l7.188 2.446a7.06 7.06 0 0 0-13.713-3l-3.003 7.705 9.219 3.456c.332.19.696.328 1.084.407.176.035.355.063.539.073a3.69 3.69 0 0 0 3.785-2.812l.64-1.253-7.285-2.48a2.4 2.4 0 0 1-1.497-3.044z" />
                        <path fill="#499D87"
                            d="M39.11 27.635l-7.187-2.447a2.399 2.399 0 0 0-1.546 4.542l7.285 2.48 1.126-3.091c.165-.492.268-.989.323-1.484" />
                        <path stroke="#585A5B" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M39.11 27.635l-7.187-2.447a2.399 2.399 0 0 0-1.546 4.542l7.285 2.48 1.126-3.091c.165-.492.268-.989.323-1.484z" />
                        <path stroke="#FFF" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.692"
                            d="M24.021 30.75l2.722-6.277s2.282-4.71 7.356-3.376" />
                        <path stroke="#FFF" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M2.429 57.093L4.719 45.9s.091-1.908 1.48-1.765c1.388.143 8.051.804 8.051.804M11.351 71.092s1.101-6.84 8.868-6.883M44.961 71.344s-.346-5.651 5.083-7.23M46.56 52.15l.334 10.113" />
                        <path stroke="#FFF" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.128"
                            d="M46.075 49.806l.146-2.945 4.01-.625" />
                        <path stroke="#FFF" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M24.202 37.152s1.429 9.316 10.003 10.898M22.938 33.756s-3.146 2.437-4.656 7.802" />
                        <path fill="#17C1AC"
                            d="M8.695 51.26a1.185 1.185 0 0 1-.156-.714 1.196 1.196 0 0 1 1.307-1.072 1.197 1.197 0 0 1 1.071 1.308c-.025.248-.126.48-.294.67l-.075.086-1.023 1.177-.774-1.358-.056-.097m1.266-2.94a2.357 2.357 0 0 0-2.575 2.111c-.05.492.057.98.306 1.41l.053.093 1.05 1.842s.124.258.449.29l.073.008.124.012.094.01c.324.031.497-.197.497-.197l1.39-1.6.072-.08c.328-.374.528-.83.577-1.323a2.357 2.357 0 0 0-2.11-2.575M9.92 55.43l.001-.005a.643.643 0 0 0-.59-.705.638.638 0 0 0-.714.572v.004a.643.643 0 0 0 .592.702.635.635 0 0 0 .712-.568" />
                    </g>
                </svg>

            </div>
        </div>
    </div>


    <section class=" my-4">
        <div class="container">
            <div class="row">
                <Card v-if="restaurants[0] != 'false' && loading === false" v-for="restaurant in restaurants"
                    :singleCard="restaurant">
                </Card>

                <!-- Messaggio di errore in caso non si trovassero ristoranti -->
                <div v-else class="p-0 d-flex flex-column align-items-center">
                    <div v-if="loading === false" class="fw-bold fs-4">
                        NESSUN RISULTATO
                    </div>
                    <img v-if="loading === false" class="no-match-img" src="../../public/notFoundImage.jpg" alt="">
                </div>
            </div>
        </div>
    </section>

    <SectionInfo></SectionInfo>
    <section class="py-5">
        <div class="container my-4">
            <div class="border-arrow my-5">
                <div class="d-flex">
                    <span class="bg-orange-text-white px-2">
                        CATEGORIE
                    </span>
                    <div class="arrow"></div>
                </div>
            </div>
            <div class="row g-3">
                <!-- Pizza -->
                <div class="col-sm-6 col-md-4 col-lg-2">
                    <div class="card card-clickable">
                        <router-link :to="{ name: 'filteredRestaurants', params: { type: 'Pizza' } }"
                            class="text-decoration-none">
                            <div class="image-background" style="background-image: url('../../public/pizza.jpeg')">
                                <h5 class="card-title text-center">Pizza</h5>
                            </div>
                        </router-link>
                    </div>
                </div>
                <!-- Sushi -->
                <div class="col-sm-6 col-md-4 col-lg-2 ">
                    <div class="card card-clickable">
                        <router-link :to="{ name: 'filteredRestaurants', params: { type: 'Sushi' } }"
                            class="text-decoration-none">
                            <div class="image-background" style="background-image: url('../../public/sushi.jpeg')">
                                <h5 class="card-title text-center">Sushi</h5>
                            </div>
                        </router-link>
                    </div>
                </div>
                <!-- Hamburger -->
                <div class="col-sm-6 col-md-4 col-lg-2 ">
                    <div class="card card-clickable">
                        <router-link :to="{ name: 'filteredRestaurants', params: { type: 'Hamburger' } }"
                            class="text-decoration-none">
                            <div class="image-background" style="background-image: url('../../public/hamburger.jpeg')">
                                <h5 class="card-title text-center">Hamburger</h5>
                            </div>
                        </router-link>
                    </div>
                </div>
                <!-- Poke -->
                <div class="col-sm-6 col-md-4 col-lg-2 ">
                    <div class="card card-clickable">
                        <router-link :to="{ name: 'filteredRestaurants', params: { type: 'Poke' } }"
                            class="text-decoration-none">
                            <div class="image-background" style="background-image: url('../../public/poke.avif')">
                                <h5 class="card-title text-center">Poke</h5>
                            </div>
                        </router-link>
                    </div>
                </div>
                <!-- Cinese -->
                <div class="col-sm-6 col-md-4 col-lg-2 ">
                    <div class="card card-clickable">
                        <router-link :to="{ name: 'filteredRestaurants', params: { type: 'Cinese' } }"
                            class="text-decoration-none">
                            <div class="image-background" style="background-image: url('../../public/cinese.jpeg')">
                                <h5 class="card-title text-center">Cinese</h5>
                            </div>
                        </router-link>
                    </div>
                </div>
                <!-- Indiano -->
                <div class="col-sm-6 col-md-4 col-lg-2 ">
                    <div class="card card-clickable">
                        <router-link :to="{ name: 'filteredRestaurants', params: { type: 'Indiano' } }"
                            class="text-decoration-none">
                            <div class="image-background" style="background-image: url('../../public/indianobuono.jpg')">
                                <h5 class="card-title text-center">Indiano</h5>
                            </div>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="pt-3">
        <div class="container">
            <div class="border-arrow my-5">
                <div class="d-flex">
                    <span class="bg-orange-text-white px-2">
                        VEDI TUTTO
                    </span>
                    <div class="arrow"></div>
                </div>
            </div>

            <div class="row my-4 g-2">
                <div class="col-sm-12 col-md-3 position-relative overflow-hidden">
                    <img class="img-style img-transform" src="../../public/img-destra.jpg" alt="">
                </div>
                <div class="col-sm-12 col-md-6 position-relative overflow-hidden">
                    <img class="img-style img-transform" src="../../public/foto-centrale.jpg" alt="">
                </div>
                <div class="col-sm-12 col-md-3 position-relative overflow-hidden">
                    <img class="img-style img-transform" src="../../public/img-sinistra.jpg" alt="">
                </div>
            </div>

            <div class="row g-2">
                <div class="col-sm-12 col-md-6 position-relative overflow-hidden">
                    <img class="img-style img-transform" src="../../public/basso-1.jpg" alt="">
                </div>
                <div class="col-sm-12 col-md-6 position-relative overflow-hidden">
                    <img class="img-style img-transform" src="../../public/ultima.jpg" alt="">
                </div>
            </div>
        </div>

    </section>
</template>

<style lang="scss" scoped>
@use "../src/styles/partials/variable" as *;



.custom-btn {
    padding: 5px 10px;
    font-size: 14px;
    background-color: orange;
    color: #ffffff;
    border-radius: 5px;
    border: 1px solid orange;

}

.container {
    .img-transform:hover {
        transform: scale(1.03);
        cursor: pointer;
    }

    .card-clickable {
        position: relative;
        cursor: pointer;
        transition: transform 0.2s, box-shadow 0.2s;
        border-radius: 30px;
    }

    .image-background {
        position: relative;
        background-size: cover;
        background-position: center;
        text-align: center;
        color: white;
        height: 100px;
        border-radius: 30px;
        background-color: rgba(42, 44, 49, 0.6);
        background-blend-mode: overlay;
        display: flex;
        justify-content: center;
        align-items: center;

    }


    .selected {
        background-color: orange;
    }

    .card-clickable:hover {
        transform: scale(1.05);
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    }

    .card-clickable:hover .image-background {
        opacity: 0.7;
    }

    .card-clickable:active {
        transform: scale(1.03);
    }

    .no-match-img {
        width: 300px;
        aspect-ratio: 1/1;
    }

    .img-style {
        width: 100%;
        height: 300px;
        object-fit: cover;
    }
}

.custom-animation-moto {
    position: relative;
    width: 20rem;
    height: 20rem;
    animation: moveLeft 2s infinite linear;

}

@media (max-width: 500px) {
    .custom-animation-moto {
        width: 10rem;
        height: 10rem;
    }
}

@media (max-width: 400px) {
    .custom-animation-moto {
        width: 7rem;
        height: 7rem;
    }
}

@media (max-width: 300px) {
    .custom-animation-moto {
        width: 5rem;
        height: 5rem;
    }
}

@keyframes moveLeft {
    0% {
        left: -100%;
    }

    100% {
        left: 100%;
    }
}
</style>

