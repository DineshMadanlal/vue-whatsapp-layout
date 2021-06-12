<template>
  <q-item
    clickable
    @click="$emit('showEnhancedChat')"

    class="conversation-card"
    :class="{ active: isActive }"

    v-ripple:positive
  >
    <!-- Conversation Profile Picture -->
    <q-img

      :src="conversation.avatar"
      width="50px"
      height="50px"
      :alt="`${conversation.person}-profile-picture`"

      :img-style="{ 'border-radius': '100%' }"
    />

    <!-- Name and the caption -->
    <div class="name-caption-block">
      <p class="name-text">
        {{ conversation.person }}
      </p>
      <p class="caption-text ellipsis">
        {{ conversation.caption }}
      </p>
    </div>

    <q-space />

    <!-- Time and menu option -->
    <div class="time-and-menu-block">
      <p class="time-text">
        {{ conversation.time }}
      </p>
    </div>
  </q-item>
</template>

<script>
export default {
  name: 'ConversationCard',
  props: {
    conversation: {
      /** Sample conversation object
       * {
          id: Number
          person: String
          avatar: String
          caption: String
          time: String
        }
      */
      type: Object,
      default: () => {},
      required: true
    },
    isActive: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
.conversation-card {
  width: 100%;
  cursor: pointer;
  padding: 12px 16px;
  background-color: $white;

  display: flex;
  .name-caption-block {
    padding: 0px 16px;
    .name-text {
      color: rgba($color: $black, $alpha: 0.8);
      font-size: 16px;
    }
    .caption-text {
      color: rgba($color: $black, $alpha: 0.7);
      font-size: 14px;
      max-width: 270px;
    }
  }
  .time-and-menu-block {
    .time-text {
      font-size: 12px;
      color: rgba($color: $black, $alpha: 0.8);
    }
  }

  &.active {
    background-color: #ebebeb;
    .name-text {
      color: rgba($color: $black, $alpha: 1);
    }
  }
}
</style>
