<script setup>
import { useCartStore } from "@/stores/cart";

const cart = useCartStore();

defineProps({
    product: Object,
});

const calculateTotal = (priceString, quantity) => {
    const numericPrice = parseFloat(priceString.replace(/[^\d,]/g, "").replace(",", "."));
    const total = numericPrice * quantity;
    return total.toLocaleString("pt-BR", {
        style: "currency",
        currency: "BRL",
    });
};
</script>

<template>
    <div class="product-wrapper">
        <div class="img-wrapper">
            <img :src="product.image" alt="" />
        </div>
        <div class="info">
            <h4>{{ product.name }}</h4>
            <h6>Quantidade: {{ product.quantity }}</h6>
            <h3>{{ calculateTotal(product.price, product.quantity) }}</h3>
        </div>
    </div>
</template>

<style scoped>
.product-wrapper {
    display: flex;
    gap: 20px;
    width: 100%;
    min-height: 200px;
    border-bottom: 1px solid var(--surface-300);
    padding-bottom: 20px;
    margin-top: 20px;
    overflow: hidden;
}

.img-wrapper {
    max-width: 30%;
    width: 30%;
    overflow: hidden;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
}

img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 20px;
    display: block;
}

.info {
    width: 70%;

    display: flex;
    flex-direction: column;
}

h6 {
    opacity: 0.6;
}

h3 {
    margin-top: 30px;
}

@media (max-width: 1000px) {
    .img-wrapper {
        max-width: 70%;
        width: 70%;
    }
}
</style>
