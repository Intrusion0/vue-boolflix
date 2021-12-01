<template>
    <header>
        <img src="@/assets/img/netflix-logo.png" alt="logo netflix" />
        <form>
            <input type="text" name="Search" placeholder="Cerca film/serie">
        </form>
    </header>
</template>

<script>
export default {
    name: "Header",
}; 
</script>

<style scoped lang="scss">
header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #090909;
    width: 100%;
    padding: 10px 0;

    img {
        height: 45px;
        width: auto;
        margin-left: 40px;
    }

    form {
        margin-right: 30px;

        input[type=text] {
            width: 100%;
            box-sizing: border-box;
            border: 2px solid #ccc;
            color: white;
            font-size: 16px;
            background-color: #090909;
            background-image: url('../assets/img/icons-search.png');
            background-position: 10px 6px; 
            background-repeat: no-repeat;
            padding: 8px 20px 8px 45px;
        }
    }
}
</style>