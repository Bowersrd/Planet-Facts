<template>
    <div class="tab-wrapper">
        <ul class="tabs">
            <li class="tabs__tab" :class="{ 'tabs__tab--active': activeTab == 0 }" @click="changeTab(0)" :style="activeColor">
                <span class="tabs__text" :class="{ 'tabs__text--active': activeTab == 0 }" :style="activeColor">
                    <span>01</span>
                    Overview
                </span>
            </li>
            <li class="tabs__tab" :class="{ 'tabs__tab--active': activeTab == 1 }" @click="changeTab(1)" :style="activeColor">
                <span class="tabs__text" :class="{ 'tabs__text--active': activeTab == 1 }" :style="activeColor">
                    <span>02</span>
                    Structure
                </span>
            </li>
            <li class="tabs__tab" :class="{ 'tabs__tab--active': activeTab == 2 }" @click="changeTab(2)" :style="activeColor">
                <span class="tabs__text" :class="{ 'tabs__text--active': activeTab == 2 }" :style="activeColor">
                    <span>03</span>
                    Surface
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: {
            planetColor: String
        },
        data() {
            return {
                activeTab: 0,
                test: 'red'
            }
        },
        methods: {
            changeTab(index) {
                this.activeTab = index;
                this.$emit('changeTab', index);
            }
        },
        computed: {
            activeColor() {
                return {
                    '--planetColor': this.planetColor
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
@import '@/assets/scss/style.scss';

.tabs {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    border-bottom: 1px solid var(--color-primary-300);
    @include md {
        display: flex;
        flex-direction: column;
        border-bottom: none;
        gap: 1rem;
    }
    &__tab {
        text-align: center;
        padding-block: 1.25rem;
        cursor: pointer;
        transition: background-color .35s ease;
        @include md {
            padding-block: .675rem;
            padding-left: 1.25rem;
            text-align: left;
            border: 1px solid var(--color-primary-300);
            &--active {
                background-color: var(--planetColor);
            }
            &:hover {
                background-color: var(--color-primary-300);
            }
        }
    }
    &__text {
        font-size: var(--fs-200);
        font-weight: var(--fw-bold);
        letter-spacing: 1.93px;
        text-transform: uppercase;
        padding-bottom: 1.1rem;
        border-bottom: 4px solid transparent;
        transition: border-bottom .35s ease;
        @include md {
            border-bottom: none;
        }
        & span {
            display: none;
            @include md {
                display: inline;
                margin-right: 1rem;
            }
        }
        &--active {
            border-bottom: 4px solid var(--planetColor);
            @include md {
                border-bottom: none;
            }
        }
        &:hover {
            border-bottom: 4px solid var(--planetColor);
            @include md {
                border-bottom: none;
            }
        }
    }
}
</style>