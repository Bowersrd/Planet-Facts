<template>
    <div class="nav-wrapper">
        <p class="nav-title">The Planets</p>
        <div class="hamburger" :class="{ 'hamburger--active': mobileIsOpen }" @click="mobileIsOpen = !mobileIsOpen; $emit('scrollLock')">
            <span class="hamburger__line"></span>
            <span class="hamburger__line"></span>
            <span class="hamburger__line"></span>
        </div>
        <nav class="nav" :class="{ 'nav--isMobileOpen': mobileIsOpen }">
            <ul class="nav-menu">
                <li class="nav-menu__item" v-for="(planet, index) in planets" :key="planet.name" @click="$emit('changePlanet', index); mobileIsOpen = false" :style="planetColor(planet.color, index)">
                    <span class="circle" :style="{ backgroundColor: `var(--color-${planet.name.toLowerCase()})` }"></span>
                    <a href="#" class="nav-menu__link">{{ planet.name }}</a>
                    <svg xmlns="http://www.w3.org/2000/svg" width="6" height="8"><path fill="none" stroke="#FFF" opacity=".4" d="M1 0l4 4-4 4"/></svg>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
    export default {
        props: {
            planets: Array,
            activePlanet: Number
        },
        data() {
            return {
                mobileIsOpen: false
            }
        },
        methods: {
            planetColor(color, index) {
                if (index != this.activePlanet) {
                    return { '--planetActiveColor': 'transparent', '--planetColor': color }
                } else {
                    return { '--planetActiveColor': color, '--planetColor': color }
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
@import '@/assets/scss/style.scss';

.nav-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-block: 1rem;
    border-bottom: 1px solid var(--color-primary-300);
    padding-inline: 1.5rem;
    margin-inline: auto;
    @include md {
        flex-direction: column;
        padding-block: 2rem 1rem;
    }
    @include xl {
        flex-direction: row;
        padding-block: 1.25rem;
        padding-inline: 2rem;
    }
}

.nav-title {
    font-size: var(--fs-600);
    text-transform: uppercase;
    font-family: var(--ff-secondary);
    font-weight: var(--fw-regular);
    letter-spacing: -1.05px;
}

.hamburger {
    width: 1.5rem;
    display: flex;
    flex-direction: column;
    @include md {
        display: none;
    }
    &--active span {
        background: var(--color-primary-300);
    }
    &__line {
        width: 100%;
        height: 3px;
        background: var(--color-white);
        margin-bottom: .25rem;
    }
}

.nav {
    position: absolute;
    top: 3.8125rem;
    right: 100%;
    height: 100vh;
    width: 100%;
    background-color: var(--color-primary-500);
    padding-inline: 1.5rem;
    z-index: 999;
    transition: right .65s ease;
    @include md {
        position: initial;
        height: initial;
        background-color: transparent;
    }
    @include xl {
        max-width: fit-content;
    }
    &--isMobileOpen {
        right: 0;
    }
}

.nav-menu {
    padding-top: 1.5rem;
    @include md {
        display: flex;
        gap: 2rem;
        justify-content: center;
    }
    @include xl {
        justify-content: flex-start;
        padding-top: 0;
    }
    &__item {
        position: relative;
        display: flex;
        align-items: center;
        padding-block: 1.25rem;
        border-bottom: 1px solid var(--color-primary-300);
        cursor: pointer;
        @include md {
            border-bottom: 4px solid var(--planetActiveColor);
            padding-bottom: .675rem;
            transition: border-bottom .35s ease;
            &:hover {
                border-bottom: 4px solid var(--planetColor);
            }
        }
        @include xl {
            padding-block: 1.5rem .5rem;
            border-bottom: none;
            &:hover {
                border-bottom: none;
            }
            &::after {
            content: "";
            width: 100%;
            height: 4px;
            background-color: var(--planetActiveColor);
            position: absolute;
            top: -1.25rem;
            left: 0;
            transition: background-color .35s ease;
            }
            &:hover::after {
                background-color: var(--planetColor);
            }
        }
        &:last-of-type {
            border-bottom: none;
            @include md {
                border-bottom: 4px solid var(--planetActiveColor);
            }
            @include xl {
                border-bottom: none;
            }
        }
        & span {
            display: inline-block;
            width: 1.25rem;
            height: 1.25rem;
            background: white;
            border-radius: 100%;
            margin-right: 1.5rem;
            @include md {
                display: none;
            }
        }
    }
    &__link {
        color: var(--color-white);
        text-decoration: none;
        text-transform: uppercase;
        font-size: var(--fs-400);
        font-weight: var(--fw-bold);
        letter-spacing: 1.36px;
        @include md {
            font-size: var(--fs-300);
            font-weight: var(--fw-regular);
        }
        @include xl {
            font-size: var(--fs-200);
        }
    }
    & svg {
        margin-left: auto;
        margin-right: .5rem;
        @include md {
            display: none;
        }
    }
}

</style>