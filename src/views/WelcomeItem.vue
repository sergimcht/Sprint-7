<template>
    <div class="welcome">
        <h3>Welcome to</h3>
        <h1>WEB CREATORS</h1>
        <p>Press Start to create your own budget</p>
        <router-link :to="{name: 'HomeItem'}">
            <button>START</button>
        </router-link>
    </div>
</template>

<script>
export default {
}
</script>

<style>
</style>