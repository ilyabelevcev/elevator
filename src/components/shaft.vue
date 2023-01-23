<template>
    <div :id="shaft.id" class="elevator__shaft">
        <div 
            :id="shaft.currentFloor" 
            :style="[
                `transform: translateY(${shaft.distanceElevator}px)`,
                `transition: ${shaft.transitionElevator}s linear`
            ]" 
            :class="{animation: shaft.isActiveSleep}" 
            class="elevator__shaft-lift"
        >
            <div :class="{visible : this.shaft.isActiveElevator}" class="elevator__shaft-indication">
                <div class="elevator__shaft-num">{{Number(shaft.desiredFloor) + 1}}</div>
                <span :class="{up : this.shaft.upElevator}" class="elevator__shaft-direction">&#8593;</span>
                <span :class="{down : this.shaft.downElevator}" class="elevator__shaft-direction">&#8595;</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            shaft: {
                type: Object,
                required: true,
            },
        },
    }
</script>

<style lang="sass">
.elevator__shaft
    position: relative
    height: 100%
    width: 10%
    border-left: 2px solid red
    border-right: 2px solid red
    &:not(:last-child)
        margin-right: 20px
    .elevator__shaft-lift
        font-size: 20px
        width: 100%
        height: 100px
        position: absolute
        bottom: 10px
        background-color: blue
        color: white
        &.animation
            animation: indication 1s infinite
    .elevator__shaft-indication
        padding-top: 8px 
        display: flex
        flex-direction: column
        align-items: center
        justify-content: center
        visibility: hidden
        &.visible
            visibility: visible
    .elevator__shaft-direction
        display: none
        &.up,&.down
            display: block
</style>