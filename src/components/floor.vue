<template>
    <div class="elevator__floor">
        <div :id="floor.id" class="elevator__floor-wrapper">
            <div class="elevator__floor-num">{{floor.num}}</div>
            <button 
                :id="floor.id" 
                @click="gettingDistance" 
                :class="{
                    active: this.floor.isActiveMove, 
                    animation: this.floor.isActiveSleep
                }" 
                :disabled="!this.floor.isFreeFloor" 
                class="elevator__floor-btn"
            ></button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                shaft: Object,
            }
        },
        props: {
            shafts: {
                type: Array,
                required: true,
            },
            floor: {
                type: Object,
                required: true,
            },
            floors: {
                type: Array,
                required: true,
            },
        },
        methods: {
            gettingDistance(event) {
                for(let i = 0; i < this.shafts.length; i++) {
                    if(this.shafts[i].isActiveElevator == false) {

                        const $btn = event.target;
                        this.shaft = this.shafts[i]
                        this.shaft.isActiveElevator = true
                        this.shaft.desiredFloor = $btn.id;
                        const transition = Math.abs(this.shaft.currentFloor - this.shaft.desiredFloor);
                        

                        if(this.shaft.desiredFloor > this.shaft.currentFloor) {
                            this.shaft.upElevator = true
                            this.shaft.downElevator = false
                        } else {
                            this.shaft.upElevator = false
                            this.shaft.downElevator = true
                        }

                        if(this.shaft.desiredFloor == this.floor.id) {
                            this.floor.isFreeFloor = false
                            if(this.shaft.currentFloor !== this.floor.id) {
                                this.floors[this.shaft.currentFloor].isFreeFloor = true
                            } else {
                                this.floor.isFreeFloor = false
                            }
                        }

                        this.shaft.transitionElevator = transition;
                        this.shaft.distanceElevator = -(this.shaft.desiredFloor * 100);
                        if(this.floor.isActiveMove = true) {
                            setTimeout (() => {
                                this.shaft.currentFloor = $btn.id; 
                                this.floor.isActiveSleep = true
                                this.shaft.isActiveSleep = true
                                setTimeout(() => {
                                    this.floor.isActiveSleep = false
                                    this.floor.isActiveMove = false
                                    this.shaft.isActiveSleep = false
                                    this.shaft.isActiveElevator = false
                                }, 3000)
                            }, (transition * 1000))
                        }
                        break 
                    } 
                }
            }, 
        },
    }
</script>

<style lang="sass">
.elevator__floor
    width: 100%
    height: 100px
    border-bottom: 1px solid #ccc
    &:last-child
        border-top: 1px solid #ccc
    .elevator__floor-wrapper
        padding-top: 10px
        width: 5%
        display: flex
        align-items: center
        flex-direction: column
        .elevator__floor-btn
            position: relative
            border: 1px solid blue
            border-radius: 100%
            width: 25px
            height: 25px
            cursor: pointer
            &.animation
                animation: indication 1s infinite
            &.active 
                border-color: orange
            &::before
                content: ''
                position: absolute
                border-radius: 100%
                border: 5px solid blue
                top: 50%
                left: 50%
                transform: translate(-50%,-50%)
            &.active::before
                border-color: orange
</style>