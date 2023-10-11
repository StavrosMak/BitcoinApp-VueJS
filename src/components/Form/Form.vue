<template>
    <div class="currency-form-container">
        <form class="form" @submit.prevent="getBitcoinPrice">
            <h2>Bitcoin Price Converter</h2>
            <div class="input-container">
                <select class="selectionField" v-model="selectedCurrency">
                    <option v-for="currency in currencies" :key="currency.code" :value="currency.code">
                        {{ currency.flag }} {{ currency.name }}
                    </option>
                </select>
                <button type="submit">Convert</button>
            </div>
        </form>

        <div class="bitcoin-Price-Result" v-if="bitcoinPrice !== null">
            <h2>Current Bitcoin Price:</h2>
            <p>{{ bitcoinPrice }} {{ conversionCurrency }}</p>
        </div>

        <section class="avgerage-Price-section" v-if="bitcoinPrice !== null">
            <h2>Average Bitcoin Price</h2>
            <p v-for="minutes in [5, 30, 60]" :key="minutes">
                Last {{ minutes }} minutes: {{ calculateAverage(minutes) }} {{ conversionCurrency }}
            </p>
        </section>
    </div>
</template>
  


<script>
import currencies from '../../assets/data/currencies';

export default {
    name: 'FormSelection',
    data() {
        return {
            selectedCurrency: 'EUR',
            conversionCurrency: '',
            bitcoinPrice: null,
            bitcoinPrices: [],
            currencies: currencies,
        };
    },
    methods: {
        
        async getBitcoinPrice() {
            const apiUrl = `https://api.coinbase.com/v2/prices/spot?currency=${this.selectedCurrency}`;
            try {
                const response = await fetch(apiUrl);
                const data = await response.json();

                if (data) {
                    this.conversionCurrency = this.selectedCurrency;
                    this.bitcoinPrice = parseFloat(data.data.amount);
                    return this.bitcoinPrice;
                } else {
                    console.error('Data is not in the expected format');
                }
            } catch (error) {
                console.error(error);
                console.log('Error fetching data');
            }
        },
        calculateAverage(minutes) {
            const prices = this.bitcoinPrices.slice(-minutes);
            if (prices.length === 0) { return 0; }
            const sum = prices.reduce((total, price) => total + price, 0);
            return (sum / minutes).toFixed(2);
        },

        resetBitcoinPrices() {
            this.bitcoinPrices = [];
        },

        updateAverages() {
            [5, 30, 60].forEach((minutes) => this.calculateAverage(minutes));
        },

        async bitcoinPerMinute() {
            try {
                const bitcoinPrice = await this.getBitcoinPrice();
                this.bitcoinPrices.push(parseFloat(bitcoinPrice));
                this.updateAverages();
                console.log(this.bitcoinPrices);
            } catch (error) {
                console.error('Error getting Bitcoin price:', error);
            }
        },
    },
     
    mounted() {
        this.bitcoinPerMinute();
        this.intervalTimer = setInterval(this.bitcoinPerMinute, 60000);
    },
    beforeUnmount() {
        clearInterval(this.intervalTimer);
    },
};
</script>
  
<style>
@import './Form.css';
</style>
  