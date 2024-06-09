<script setup>
import {onMounted, ref} from 'vue'


const quote = ref({
    content: '',
    author: ''
})

const isLoading = ref(false)

const BASE_URL='https://api.quotable.io'

async function getRandomQuote(){
    try {
        isLoading.value = true
        const response = await fetch(`${BASE_URL}/random`)
        if(!response.ok){
            throw new Error('Something went wrong! please try again later')
        }
        const data = await response.json()
        quote.value.content = data.content 
        quote.value.author = data.author
        isLoading.value = false
    } catch (error) {
        console.log(error)
        isLoading.value = false
    }
}

function tweet() {
    if(!quote.value.content || !quote.value.author){
        return 
    }
    window.open(
        `https://twitter.com/intent/tweet?text=${quote.value.content} --- by ${quote.value.author}`, 
        "Tweet Window", 
        "width=600, height=300"
    )
}

onMounted(() => {
    getRandomQuote()
})
</script>

<template>
    <div class="quote-card">
        <p class="quote-card-title">Quote of the day</p>
        <blockquote>
            <p class="quote" v-if="isLoading">Loading...</p>
            <h1 class="quote" v-else>"{{ quote.content }}"</h1>
            <cite v-if="isLoading">Loading...</cite>
            <cite v-else>{{ quote.author }}</cite>
        </blockquote>
        <div class="btn-wrapper">
            <button class="btn-new__quote" @click="getRandomQuote">New Quote</button>
            <button @click="tweet">
                <svg xmlns="http://www.w3.org/2000/svg" width="18px" height="18px" viewBox="0 0 32 32" fill="none">
                    <path d="M11.7887 28C8.55374 28 5.53817 27.0591 3 25.4356C5.15499 25.5751 8.95807 25.2411 11.3236 22.9848C7.76508 22.8215 6.16026 20.0923 5.95094 18.926C6.25329 19.0426 7.6953 19.1826 8.50934 18.856C4.4159 17.8296 3.78793 14.2373 3.92748 13.141C4.695 13.6775 5.99745 13.8641 6.50913 13.8174C2.69479 11.0882 4.06703 6.98276 4.74151 6.09635C7.47882 9.88867 11.5812 12.0186 16.6564 12.137C16.5607 11.7174 16.5102 11.2804 16.5102 10.8316C16.5102 7.61092 19.1134 5 22.3247 5C24.0025 5 25.5144 5.71275 26.5757 6.85284C27.6969 6.59011 29.3843 5.97507 30.2092 5.4432C29.7934 6.93611 28.4989 8.18149 27.7159 8.64308C27.7224 8.65878 27.7095 8.62731 27.7159 8.64308C28.4037 8.53904 30.2648 8.18137 31 7.68256C30.6364 8.52125 29.264 9.91573 28.1377 10.6964C28.3473 19.9381 21.2765 28 11.7887 28Z" fill="#47ACDF"/>
                </svg>
                Tweet
            </button>
        </div>
    </div>
</template>

<style scoped>
.quote-card{
    background-color: #fff;
    max-width: 650px;
    padding: 32px 80px;
    text-align: center;
    border-radius: 6px;
    box-shadow: 0px 0px 12px 2px #5757575d;
}

.quote-card-title{
    font-size: 30px;
    line-height: 180%;
    font-weight: 500;
    position: relative;
    margin-bottom: 42px;
    color: #2974DE;
}
.quote-card-title::after{
    content: '';
    display: inline-block;
    border: 2px solid #2974DE;
    height: 0;
    width: 42px;
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 4px;
}
.quote{
    margin-bottom: 24px;
    font-weight: 500;
    font-size: 38px;
    letter-spacing: 0.4px;
    font-style: italic;
}
cite{
    font-style: normal;
    display: flex;
    align-items: center;
    gap: 4px;
    font-weight: 400;
    justify-content: end;
    color: #2974DE;
    font-size: 14px;
}
cite::before{
    content: '';
    display: inline-block;
    border: 1px solid #2974DE;
    height: 0;
    width: 16px;
    border-radius: 2px;
}
blockquote{
    margin-bottom: 42px;
}
button{
    padding: 12px 32px;
    border-radius: 32px;
    border: 1px solid #2974DE;
    font-size: 16px;
    background-color: transparent;
    color: #2974DE;
    transition: all ease 0.35s;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 6px;
}
button:hover{
    background-color: #2974DE;
    color: #fff;
}
button svg path{
    transition: all ease 0.35s;
    fill: #2974DE;
}
button:hover svg path{
    fill: #fff;
}
button:focus{
    background-color: transparent;
    color: #2974DE;
}
button:focus svg path {
    fill: #2974DE;
}
.btn-wrapper{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 18px;
}
.btn-new__quote{
    background-color: #2974DE;
    color: #fff;
}
.btn-new__quote:hover{
    background-color: transparent;
    color: #2974DE;
}
.btn-new__quote:focus{
    background-color: #2974DE;
    color: #fff;
}
</style>