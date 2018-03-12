<template lang="html">
    <header>
        <div class="upperHeader">
            <div class="title">
                <h1>Football Scores</h1>
            </div>
            <nav>
                <a href="#">
                    <img src="/images/pl_white.png" alt="">
                </a>
                <a href="#">
                    <img src="/images/la_liga_logo.png" alt="">
                </a>
                <a href="#">
                    <img src="/images/serie-a-logo.png" alt="">
                </a>
                <a href="#">
                    <img src="/images/ligue1_logo.png" alt="">
                </a>
                <a href="#">
                    <img src="/images/Bundesliga_Logo.png" alt="">
                </a>
                <a href="#">
                    <img src="/images/Primeira_Liga_Logo.png" alt="">
                </a>
                <a href="#">
                    <img src="/images/eredivisie_logo.png" alt="">
                </a>
            </nav>
        </div>
    </header>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>

header {
    padding: 10px 100px;
    margin: 0;
    background-color: #212121;
    border-bottom: 1px solid #f00;

    .upperHeader {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0;

        nav {
            display: flex;
            align-items: center;

            a {
                display: block;
                text-align: center;
                color: #212121;
                text-decoration: none;
                margin: 0 20px;

                &:last-of-type {
                    margin-right: 0;
                }

                img {
                    width: 40px;
                    height: auto;
                }

                p {
                    text-transform: uppercase;
                    margin: 0;
                }
            }
        }
    }
}
</style>
