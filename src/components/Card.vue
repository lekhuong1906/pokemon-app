<template>
    <div class="card" :class="{ disabled: isDisbaled }" :style="{
        height: `${(920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
        width: `${((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3 / 4}px`,
        perspective: `${(((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3 / 4) * 2}px`
    }">
        <div class="card__inner" :class="{ 'is-flipped': isFlipped }" @click="onToggleFlipCard">
            <div class="card__face card__face--front">
                <div class="card__content"></div>
            </div>
            <div class="card__face card__face--back">
                <div class="card__content" >
                    <img class="card__content--img" :src="imgBackFaceUrl">
                </div>
            </div>
        </div>
    </div>
</template> 

<script>

export default {
    props: {
        card: {
            type: [String, Number, Array, Object],
            requied: true,
        },
        imgBackFaceUrl: {
            type: String,
            required: true,
        },
        cardsContext: {
            type: String,
            requied: true,
            default: () => {
                return [];
            }
        }
    },
    data() {
        return {
            isDisbaled: false,
            isFlipped: false,
        }
    },
    methods: {
        onToggleFlipCard() {
            if (this.isDisbaled) {
                return false;
            }
            this.isFlipped = !this.isFlipped;
            if (this.isFlipped) {
                this.$emit('onFlip', this.card)
            }
        },
        onFlipBackCard() {
            this.isFlipped = false;
        },
        onEnabledDisabledMode() {
            this.isDisbaled = true;
        }
    }
}
</script>


<style lang="css" scoped>
.card {
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
    width: 90px;
    height: 120px;
}

.card__inner {
    width: 100%;
    height: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
}

.card__content--img {
    width: 100%;
    height: 100%;
}

.card__inner.is-flipped {
    transform: rotateY(-180deg);
}

.card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__face--front .card__content {
    background: url('/images/icon_back.png') no-repeat center center;
    background-size: 60%;
    height: 100%;
    width: 100%;
}

.card__face--back {
    background-color: var(--light);
    transform: rotateY(-180deg);
}

.card__face--back .card__content {
    background-size: contain;
    background-position: center center;
    background-repeat: no-repeat;
    height: 100%;
    width: 100%;
}

.card.disabled .card__inner {
    cursor: default;
}
</style>