<template>
<div class="channel-message" :class="{ hasMention: hasMention }">
    <img v-if="isBot" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/discord-logo.svg" alt="dicord-logo" />
    <img v-else-if="isHarry" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/harry.jpg" alt="harry" />
    <img v-else-if="isOkakoro" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/pedo.jpg" alt="okakoro" />
    <img v-else-if="isInu" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/inu.png" alt="inu" />
    <img v-else-if="isToki" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/discord-logo.svg" alt="toki" />
    <img v-else-if="isHaru" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/haru.png" alt="haru" />
    <img v-else-if="isOi" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/oi.png" alt="oi" />
    <img v-else-if="isKuro" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/kuro.jpg" alt="kuro" />
    <img v-else-if="isGin" style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/gin.jpg" alt="gin" />
    <img v-else style="width: 48px; height: 48px; display: flex; margin-left: 10px; margin-right: 10px;" src="../../assets/images/tmchvd circle.png" alt="tmchvd" />
    <div class="message">
        <div class="user">
            <strong>{{ authorName }}</strong>
            <span class="bot" v-if="isBot">bot</span>
            <span class="date">{{ date }}</span>
        </div>
        <div class="body">
            <slot />
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: {
        authorName: String,
        date: String,
        hasMention: Boolean,
        isBot: Boolean,
        isHarry: Boolean,
        isOkakoro: Boolean,
        isInu: Boolean,
        isToki: Boolean,
        isHaru: Boolean,
        isOi: Boolean,
        isKuro: Boolean,
        isGin: Boolean,
    },
}
</script>

<style lang="scss" scoped>
.channel-message {
    box-sizing: content-box;
    display: flex;
    padding: 8px 16px;
    margin-right: 4px;
    background-color: transparent;
    margin-top: 5px;

    &.hasMention {
        background-color: var(--mention-message);
        border-left: solid 2px var(--mention-detail);
    }

    &:hover {
        background-color: var(--tertiary);

        .avatar {
            transition: all 0.2s;
            background-color: var(--primary);
        }
    }
}

.avatar {
    top: 5px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: var(--secondary);
    flex-shrink: 0;

    &.botAvatar {
        background-color: var(--mention-detail);
        background-image: url('../../assets/images/tmchvd circle.png');
    }
}

.message {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-left: 17px;

    strong {
        color: var(--white);
        font-size: 16px;
        letter-spacing: 1px;
    }

    .date {
        margin-left: 6px;
        color: var(--grey);
        font-size: 13px;
    }

    .body {
        color: var(--white);
        text-align: left;
        font-size: 16px;
        margin-top: 5px;
    }

    .bot {
        margin-left: 9px;
        background-color: var(--discord);
        padding: 4px 5px;
        text-transform: uppercase;
        font-size: 11px;
        font-weight: bold;
        color: var(--white);
        border-radius: 4px;
    }
}
</style>
