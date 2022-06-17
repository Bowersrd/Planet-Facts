<template>
    <div class="planet">
        <tab-navigation class="tab-nav" :planetColor="planet.color" @change-tab="changeTab"></tab-navigation>
        <div class="planet__image-container">
            <img :src="require(`@/assets/images/planets/planet-${planet.name.toLowerCase()}.svg`)" :alt="`Illustration of ${planet.name}`" v-show="currentView != 'structure'">
            <img :src="require(`@/assets/images/planets/planet-${planet.name.toLowerCase()}-internal.svg`)" :alt="`Illustration of ${planet.name}`" v-show="currentView == 'structure'">
            <img class="planet__geology" :src="require(`@/assets/images/planets/geology-${planet.name.toLowerCase()}.png`)" :alt="`Illustration of ${planet.name}`" v-show="currentView == 'geology'">
        </div>
        <div class="planet__info">
            <h1 class="planet__name">{{ planet.name }}</h1>
            <p class="planet__description">{{ planet[currentView].content }}</p>
            <p class="planet__source">
                Source: <a :href="planet[currentView].source" target="_blank" class="planet__source--link">Wikipedia</a>
                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12"><path fill="#FFF" d="M11.34.66C10.9.22 10.37 0 9.75 0h-7.5C1.63 0 1.1.22.66.66.22 1.1 0 1.63 0 2.25v7.5c0 .62.22 1.15.66 1.59.44.44.97.66 1.59.66h7.5c.62 0 1.15-.22 1.59-.66.44-.44.66-.97.66-1.59v-7.5c0-.62-.22-1.15-.66-1.59zM10 6.25a.467.467 0 01-.305.46.544.544 0 01-.195.04.465.465 0 01-.352-.149L8.023 5.476 3.852 9.648a.481.481 0 01-.352.149.48.48 0 01-.352-.149l-.796-.797a.48.48 0 01-.149-.351.48.48 0 01.149-.352l4.172-4.172-1.125-1.125c-.162-.15-.198-.333-.11-.546A.467.467 0 015.75 2H9.5c.135 0 .253.05.352.148A.48.48 0 0110 2.5v3.75z" opacity=".5"/></svg>
            </p>
        </div>
    </div>
</template>

<script>
    import tabNavigation from '@/components/TabNavigation';
    export default {
        components: {
            tabNavigation
        },
        props: {
            planet: Object,
            currentView: String
        },
        methods: {
            changeTab(index) {
                this.$emit('changeTab', index);
            }
        }
    }
</script>

<style lang="scss" scoped>
@import '@/assets/scss/style.scss';

.planet {
    max-width: 90rem;
    width: 100%;
    text-align: center;
    overflow: hidden;
    margin-inline: auto;
    @include md {
        display: grid;
        grid-template-columns: 60% 1fr;
        text-align: left;
        align-items: center;
    }
    @include xl {
        grid-template-columns: 65.5% 1fr;
        padding-inline: 165px;
        gap: 0 1.5rem;
    }
    &__image-container {
        position: relative;
        height: 16rem;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 1.5rem;
        @include md {
            height: 26.375rem;
            grid-column: span 2;
            grid-row: 1 / 1;
        }
        @include xl {
            height: 41.625rem;
            grid-column: span 1;
            grid-row: 1 / 3;
        }
        & img {
            transform: scale(.3825);
            @include md {
                transform: scale(.635);
            }
            @include xl {
                transform: scale(1);
            }
        }
    }
    &__info {
        @include md {
            grid-column: span 1;
            grid-row: 2 / 3;
            padding-inline: 2.5rem;
        }
        @include xl {
            grid-row: 1 / 2;
            align-self: end;
            justify-self: end;
            padding-inline: 0;
        }
    }
    &__name {
        font-family: var(--ff-secondary);
        text-transform: uppercase;
        font-size: var(--fs-700);
        margin-bottom: 1rem;
        @include md {
            margin-bottom: 1.5rem;
        }
    }
    &__description {
        max-width: 33ch;
        font-size: var(--fs-300);
        line-height: 2.2;
        font-weight: var(--fw-light);
        margin-bottom: 2rem;
        margin-inline: auto;
        @include md {
            margin-inline: initial;
            max-width: 35ch;
        }
        @include lg {
            max-width: 45ch;
        }
    }
    &__source {
        font-size: var(--fs-300);
        opacity: 50%;
        font-weight: var(--fw-regular);
        letter-spacing: 1px;
        margin-bottom: 1.75rem;
        @include xl {
            margin-bottom: 2.5rem;
        }
        &--link {
            color: var(--color-white);
            font-weight: var(--fw-bold);
            text-decoration: underline;
            cursor: pointer;
            transition: color .25s ease;
            &:hover {
                color: var(--color-primary-100);
            }
        }
        & svg {
            margin-left: .5rem;
        }
    }
    &__geology {
        position: absolute;
        top: 8rem;
        height: 75%;
        @include md {
            top: 16rem;
            height: 50%;
        }
        @include xl {
            top: 27rem;
            height: 25%;
        }
    }
}

.tab-nav {
    @include md {
        grid-column: span 1;
        padding-right: 2.5rem;
    }
    @include xl {
        grid-column: 2 / -1;
        align-self: start;
        padding-right: 0;
    }
}
</style>