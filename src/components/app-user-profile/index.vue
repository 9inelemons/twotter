<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">
                @{{ user.username }}
            </h1>
            <div
                v-if="user.isAdmin"
                class="user-profile__admin-badge"
            >
                Admin
            </div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong> {{ followers }}
            </div>
            <form
                class="user-profile__create-twoot"
            >
                <label for="newTwoot">
                    <strong>New Twoot</strong>
                </label>

                <textarea id="newTwoot" rows="4"></textarea>

                <div class="user-profile__create-twoot-type">
                    <label for="newTwootType">
                        <strong>Type: </strong>
                    </label>

                    <select id="newTwootType">
                        <option
                            v-for="type in twootTypes"
                            :key="type.id"
                            :value="type.value"
                        >
                            {{ type.name }}
                        </option>
                    </select>
                </div>
            </form>
        </div>
        <div class="user-profile__twoots-wrapper">
            <app-twoot-item
                v-for="twoot in user.twoots"
                :key="twoot.id"
                :username="user.username"
                :twoot="twoot"
                @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
    import AppTwootItem from '@/components/app-twoot-item';

    export default {
        name: 'app-user-profile',

        components: {
            AppTwootItem,
        },

        data() {
            return {
                twootTypes: [
                    {
                        value: 'draft',
                        name: 'Draft',
                        id: 1,
                    },
                    {
                        value: 'instant',
                        name: 'Instant Twoot',
                        id: 2,
                    },
                ],

                followers: 0,

                user: {
                    id: 1,
                    username: '_9inelemons',
                    firstName: 'Vladislav',
                    lastName: 'Kosarev',
                    email: '9inelemons@gmail.com',
                    isAdmin: true,
                    twoots: [
                        {
                            id: 1,
                            content: 'Twotter is Amazing!',
                        },
                        {
                            id: 2,
                            content: 'Whoops!',
                        },
                    ],
                },
            };
        },

        computed: {
            fullName() {
                return `${ this.user.firstName } ${ this.user.lastName }`;
            },
        },

        watch: {
            followers(newVal, oldVal) {
                if (oldVal < newVal) {
                    console.log(`${ this.user.username } has gained a follower!`);
                }
            },
        },

        mounted() {
            this.followUser();
        },

        methods: {
            followUser() {
                this.followers++;
            },

            toggleFavourite(id) {
                console.log(`Favourited Twoot #${ id }`);
            },
        },
    };
</script>

<style>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        width: 100%;
        padding: 50px 5%;
    }

    .user-profile__user-panel {
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #DFE3E8;
    }

    .user-profile__admin-badge {
        background: purple;
        color: white;
        border-radius: 5px;
        margin-right: auto;
        padding: 0 10px;
        font-weight: bold;
    }

    .user-profile__twoots-wrapper {
        display: grid;
        grid-gap: 10px;
    }

    .user-profile__create-twoot {
        border-top: 1px solid #DFE3E8;
        padding-top: 20px;
        display: flex;
        flex-direction: column;
    }

    h1 {
        margin: 0;
    }
</style>
