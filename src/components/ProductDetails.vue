<template>
    <div class="products">
        <div class="product" v-for="product in products" :key="product.id">
            <h3>{{ product.name }}</h3>
            <p>${{ (product.price / usd).toFixed(2) }}</p>
            <!-- <p>${{ formattedPrice }}</p> -->
            <p>
                {{ product.available ? "Available" : "Out of stock" }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ProductComp',
  
    data() {
        return {
            products: [
                {
                    id: 1,
                    name: "Product 1",
                    price: 17.00,
                    available: true
                },
                {
                    id: 2,
                    name: "Product 2",
                    price: 199.99,
                    available: false
                },
                {
                    id: 3,
                    name: "Product 3",
                    price: 230.70,
                    available: true
                },
                {
                    id: 4,
                    name: "Product 4",
                    price: 50.54,
                    available: true
                },
            ],
            usd: 0,
        };
    },
  
    mounted() {
        fetch('https://www.cbr-xml-daily.ru/daily_json.js')
            .then(data => data.json())
            .then(responce => {
                this.usd = responce.Valute.USD.Value;
            })
        },

    methods: {
        
    },

    // НЕ РАБОТАЕТ!
    computed: {
        formattedPrice: function() {
            const formatter = (this.price / this.usd).toFixed(2);
            return formatter;
        },
    },
}

</script>
    
<style scoped>
    .products {
        display: flex;
        gap: 30px;
    }

    .product {
        width: 200px;
        height: 150px;
        border: 1px solid rgb(10, 12, 124);
    }
</style>