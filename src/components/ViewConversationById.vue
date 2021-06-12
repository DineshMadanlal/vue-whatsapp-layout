<template>
  <div class="view-conversation-by-id">
    <!-- Layout -->
    <q-layout
      container
      view="lHh lpR lFf"
      class="conversation-layout"

      v-if="conversation.id"
    >
      <q-header class="chat-header flex no-wrap items-center">
        <q-img
          :src="conversation.avatar"
          width="40px"
          height="40px"
          :alt="`${conversation.person}-user-profile-picture`"

          :img-style="{ 'border-radius': '100%' }"
        />
        <!-- Name -->
        <p class="name-text">
          {{ conversation.person }}
        </p>

        <q-space />

        <!-- Status icon -->
        <q-btn
          flat
          dense
          rounded
          unelevated

          color="positive"
        >
          <img
            svg-inline
            src="assets/icons/search.svg"

            class="no-outline search-icon"
          />
        </q-btn>

        <!-- Menu icon -->
        <div class="no-line-height">
          <q-btn
            flat
            dense
            rounded
            unelevated

            color="positive"
          >
            <img
              svg-inline
              src="assets/icons/menu.svg"

              class="no-outline menu-icon"
            />
          </q-btn>
        </div>
      </q-header>

      <!-- Content -->
      <q-page-container>
        <q-page class="conversation-messages-section">
          <div class="background-img-section" />
        </q-page>
      </q-page-container>

      <!-- Footer -->
      <q-footer class="conversation-footer">
        <q-input
          v-model="message"

          dense
          outlined
          rounded

          placeholder="Type a message"

          class="message-input"
        />
      </q-footer>
    </q-layout>

    <!-- Empty illustration -->
    <div v-else class="empty-illustration">
      <img
        src="~/assets/illustrations/intro-connection.jpeg"
        class="no-outline"
        height="355px"
        width="355px"
      />

      <h3 class="phone-connected-text">
        Keep your phone connected
      </h3>

      <p class="whatsapp-security-text">
        WhatsApp connects to your phone to sync messages. To reduce data usage, connect your phone to Wi-Fi.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ViewConversationById',
  data () {
    return {
      message: ''
    }
  },
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
    }
  }
}
</script>

<style lang="scss" scoped>
.view-conversation-by-id {
  width: 100%;
  min-height: inherit;
  .conversation-layout {
    min-height: inherit;
    .chat-header {
      z-index: 3;

      height: 60px;
      padding: 10px 16px;
      background-color: $grey-dark;
      .name-text {
        color: rgba($color: $black, $alpha: 1);
        font-size: 16px;
        margin-left: 12px;
        font-weight: 450;
      }
      .search-icon, .menu-icon {
        path {
          fill: grey;
        }
      }
    }
    .conversation-messages-section {
      .background-img-section {
        min-height: inherit;
        background-image: url('../assets/illustrations/bg-chat-tile.png');
        background-size: 412.5px 749.25px;
        opacity: 0.06;
      }
    }
    .conversation-footer {
      height: 60px;
      padding: 10px 16px;
      background-color: $grey-dark;
    }
  }

  .empty-illustration {
    width: 100%;
    min-height: inherit;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;

    background-color: #f8f9fb;

    .phone-connected-text {
      margin-top: 36px;
      font-size: 36px;
      font-weight: 300;
      color: #525252;
      margin-bottom: 24px;
    }
    .whatsapp-security-text {
      font-size: 14px;
      line-height: 20px;
      color: rgba($color: $black, $alpha: 0.45);
      max-width: 460px;
      text-align: center;
    }
  }
}
</style>

<style lang="scss">
.view-conversation-by-id {
  .conversation-layout {
    .message-input {
      .q-field__control {
        background: $white;
      }
    }
  }
}
</style>
