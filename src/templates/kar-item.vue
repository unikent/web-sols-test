<template>
    <li class="KARitem">
        <span v-html="data.citations.APA"></span>
        <div class="KARlinks">
            <div>
                <button @click="show = !show" class="abstractBtn KARlink">
                Abstract
                <i class="abstractIcon down"></i></button>
                <a :href="data.kar_url" target="_blank" class="KARExternal KARlink">View in KAR</a>
            </div>
            <p v-show="show">{{ data.abstract }}</p>
        </div>
   </li>
</template>

<script>
export default {
    name: 'karitem',
    props: {
        data: Object
    },
    data() {
        return {
            show: false
        }
    }
}
</script>