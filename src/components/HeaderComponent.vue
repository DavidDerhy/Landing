<template>
    <div class="pos-header">
        <ul>
            <template v-for="item in menuItem">
                <template v-if="item.link === null">
                    <li>{{ item.name }}</li>
                </template>
                <template v-if="item.link !== null">
                    <router-link :to="{ name: item.link }">{{item.name}}</router-link>
                </template>
            </template>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'HeaderComponent',
        data: () => {
            return {
                menuItem: [
                    {
                        name: 'Delegation',
                        link: null,
                    },
                    {
                        name: 'Buy Tezos',
                        link: null,
                    },
                    {
                        name: 'Guides',
                        link: null,
                    },
                    {
                        name: 'Contact',
                        link: null,
                    },
                    {
                        name: 'Dashboard',
                        link: 'dashboard',
                    },
                ],
            };
        },
        watch: {
            $route(to, from) {
                if (to.name === 'dashboard') {
                    this.setButtonHome();
                }
                if (from.name !== null) {
                    this.toggleButton(from.name);
                }
            },
        },
        methods: {
            setButtonHome() {
                this.menuItem[4].name = 'Back to Home';
                this.menuItem[4].link = 'home';
            },
            toggleButton(navigation) {
                this.menuItem[4].name = navigation;
                this.menuItem[4].link = navigation;
            },
        },
    };
</script>

<style scoped lang="scss">
    .pos-header {
        ul {
            display: flex;
            max-width: 1240px;
            margin: 30px auto 0 auto;
            width: 96%;
            height: 40px;
            align-items: center;
            font-size: 20px;
            cursor: pointer;
            color: #000000;

            li {
                margin: 0 22px;

                &:hover {
                    color: #3672F8
                }
            }

            a {
                margin-left: auto;
                background: #7495D7;
                padding: 10px 52px;
                border-radius: 10px;
                color: #ffffff;

                &:hover {
                    color: #000000;
                    background: #ffffff;
                    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
                }
            }
        }
    }
</style>
