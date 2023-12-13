<template>
    <ul class="nav nav-tabs">
        <li class="nav-item">
            <router-link class="nav-link" to="/" activeClass="active">Home</router-link>
        </li>
        <li class="nav-item">
            <router-link class="nav-link" to="/todo" activeClass="active">ToDo</router-link>
        </li>
        <li class="nav-item">
            <router-link class="nav-link" to="/clicker" activeClass="active">Clicker</router-link>
        </li>
    </ul>
</template>

<style>
.nav {
    background-color: bisque;
}
</style>

<script>
export default {

}
</script>