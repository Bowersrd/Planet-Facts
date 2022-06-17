<template>
    <div class="stats">
        <div class="stat">
            <p class="stat__title">Rotation Time</p>
            <p class="stat__value">{{ planet.rotation }}</p>
        </div>
        <div class="stat">
            <p class="stat__title">Revolution Time</p>
            <p class="stat__value">{{ planet.revolution }}</p>
        </div>
        <div class="stat">
            <p class="stat__title">Radius</p>
            <p class="stat__value">{{ planet.radius }}</p>
        </div>
        <div class="stat">
            <p class="stat__title">Average Temp.</p>
            <p class="stat__value">{{ planet.temperature }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            planet: Object
        }
    }
</script>

<style lang="scss" scoped>
@import '@/assets/scss/style.scss';

.stats {
    max-width: 90rem;
    padding-inline: 1.5rem;
    display: flex;
    flex-direction: column;
    gap: .5rem;
    margin-bottom: 3rem;
    margin-inline: auto;
    @include md {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        padding-inline: 2.5rem;
        flex-direction: row;
        margin-bottom: 2.25rem;
    }
    @include xl {
        gap: 1.875rem;
        padding-inline: 165px;
    }
}

.stat {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 1px solid var(--color-primary-300);
    padding: .625rem 1.5rem;
    @include md {
        flex-direction: column;
        align-items: flex-start;
        padding: 1rem 1rem 1.2rem;
    }
    &__title {
        font-size: var(--fs-100);
        letter-spacing: 1px;
        text-transform: uppercase;
        opacity: 50%;
        @include md {
        font-size: var(--fs-100);
        margin-bottom: .75rem;
        }
    }
    &__value {
        font-family: var(--ff-secondary);
        font-size: var(--fs-500);
    }
}
</style>