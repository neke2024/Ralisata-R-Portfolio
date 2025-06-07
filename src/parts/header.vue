<template>
    <div class="Header">
        <div class="container">
            <div class="left"><img src="../assets/logo.png" alt="me logo"></div>
            <div class="right">
                <nav>
                    <ul>
                        <li><a href="#">Begin</a></li>
                        <li><a href="#">About Me</a></li>
                        <li><a href="#">Contact-Me</a></li>
                    </ul>
                    <button type="button">Telecharger mon CV</button>
                </nav>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: "Header",
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Audiowide&family=Syncopate:wght@400;700&display=swap');

.Header {
    background: #171810;
    color: #fff;
    padding: 20px 10px;
    height: 70px;
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100%;
}

.left {
    flex: 1;
}

.right {
    flex: 2;
    display: flex;
    justify-content: flex-end;
}

.left img {
    height: 100px;
    width: auto;
    display: block;
    padding: 0px 30px;
    border-radius: 30px;
}

nav {
    display: flex;
    align-items: center;
}

ul {
    list-style: none;
    display: flex;
    margin: 0;
    padding: 0;
}

li {
    margin-right: 20px;
}

a {
    font-family: "Syncopate", sans-serif;
    color: #ffffff70;
    text-decoration: none;
    font-weight: bold;
    transition: color 0.2s;
}

a:hover {
    color: #D40000FF;
}

button {
    background: #D40000FF;
    color: #fff;
    border: none;
    padding: 8px 18px;
    border-radius: 4px;
    cursor: pointer;
    font-family: "Audiowide", sans-serif;
    font-size: 15px;
    /* font-weight: bold; */
    transition: background 0.2s;
}

button:hover {
    background: #A70000FF;
}
</style>