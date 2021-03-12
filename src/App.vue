<template>
    <div id="app">
        <app-user-profile />
    </div>
</template>

<script>
    import AppUserProfile from '@/components/app-user-profile';

    export default {
        name: 'app',
        components: {
            AppUserProfile,
        },
    };
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        min-height: 100vh;
        background-color: #F3F5FA;
    }
</style>
