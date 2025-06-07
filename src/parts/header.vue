<template>
    <div class="Header">
        <div class="container">
            <div class="left"></div>
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
.Header {
    background: #222;
    color: #fff;
    padding: 20px 10px;
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.left {
    flex: 1;
}

.right {
    flex: 2;
    display: flex;
    justify-content: flex-end;
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
    color: #fff;
    text-decoration: none;
    font-weight: bold;
    transition: color 0.2s;
}

a:hover {
    color: #00bcd4;
}

button {
    background: #00bcd4;
    color: #fff;
    border: none;
    padding: 8px 18px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
    transition: background 0.2s;
}

button:hover {
    background: #0097a7;
}
</style>