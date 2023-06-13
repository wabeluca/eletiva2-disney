<template>
    <header>
        <nav>
            <RouterLink to="/">Principal</RouterLink>
            <RouterLink to="/about">About</RouterLink>
            <router-link to="/teste">Teste</router-link>
        </nav>
    </header>
</template>

<script>
export default {
    name: 'Menu'
}
</script>

<style scoped>
    header {
        background-color: rgb(255, 255, 255);
        display: flex;
        justify-content: flex-end;
        height: 30px;
        color: rgb(28, 17, 4);
        padding: 20px;
        align-items: center;
    }
    a {
        text-decoration: none;
        margin: 20px;
        font-size: 16px;
    }
    a:hover {
        font-size: 20px;
    }
</style>