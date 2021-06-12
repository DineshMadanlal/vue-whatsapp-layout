<template>
  <!-- Whatsapp layout -->
  <q-layout view="lHh lpR lFf" class="vue-whatsapp-layout">
    <!-- Left sidebar/drawer -->
    <q-drawer
      :width="430"
      v-model="leftDrawerOpen"

      bordered
      show-if-above

      side="left"
      class="whatsapp-sidebar"
    >
      <!-- Sticky header in the drawer. Here we show,
        1. User profile picture
        2. Enable Desktop Notification
        3. Search option
      -->
      <div
        class="absolute-top sidebar-header-wrapper"

        :style="{ height: '200px' }"
      >
        <!-- NOTE: We have a fixed height here because the below scroll content will have
        a padding top of the same height which is 200px. since we do absolute positioning for
        the header. -->

        <!-- User Profile Block -->
        <div class="user-profile-block">
          <!-- Profile picture of the user -->
          <q-img

            src="https://miro.medium.com/fit/c/1360/1360/1*YPNsXXFILEUnKLiw3OdpIg.jpeg"
            width="40px"
            height="40px"
            alt="user-profile-picture"

            :img-style="{ 'border-radius': '100%' }"
          />

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
              src="assets/icons/status.svg"

              class="no-outline status-icon"
            />
          </q-btn>
          <!-- Chat icon -->
          <q-btn
            flat
            dense
            rounded
            unelevated
            class="q-ml-md q-mr-sm"

            color="positive"
          >
            <img
              svg-inline
              src="assets/icons/chat.svg"

              class="no-outline chat-icon"
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
        </div>

        <!-- Desktop Notification Block -->
        <div class="desktop-notification-block">
          <!-- Notification Icon -->
          <img
            svg-inline
            src="assets/icons/notification.svg"

            class="notification-icon"
          />

          <div>
            <p class="desktop-label-text">
              Get notified of new messages
            </p>
            <p class="desktop-action-text">
              Turn on desktop notifications
            </p>
          </div>
        </div>

        <!-- Search Chat Block -->
        <div class="search-chat-block">
          <!-- filter conversation text -->
          <q-input
            v-model="conversationFilterText"

            outlined
            rounded
            dense
            placeholder="Search or start a new chat"

            class="filter-input"
          />
        </div>

      </div>

      <!-- Chats -->
      <q-scroll-area
        style="height: calc(100vh - 200px); margin-top: 200px;"
        class="all-conversations"
      >
        <!-- Conversation card reuable component -->
        <ConversationCard
          v-for="(eachConversation, index) in conversations"
          :key="`each-conversation-${eachConversation.id}-${index}`"

          :conversation="eachConversation"
          :isActive="activeConversation.id === eachConversation.id"

          @showEnhancedChat="activeConversation = eachConversation"
        />
      </q-scroll-area>
    </q-drawer>

    <!-- Page container content -->
    <q-page-container>
      <q-page>
        <ViewConversationById
          :conversation="activeConversation"
        />
      </q-page>
    </q-page-container>

  </q-layout>
</template>

<script>
// Constants
import { CONVERSATIONS } from 'boot/constants'

export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: true, // state variable to open/close the sidebar
      conversationFilterText: '', // filter conversation text
      activeConversation: {}
    }
  },
  components: {
    // lazy load components - same as how we lazy load pages in routes
    ConversationCard: () => import('components/ConversationCard'),
    ViewConversationById: () => import('components/ViewConversationById')
  },
  computed: {
    // ---- STATIC DATA BEGIN ----
    conversations () {
      if (this.conversationFilterText) {
        /** Filter with caption or name */
        const lowerCaseFilter = this.conversationFilterText.toLowerCase()
        return CONVERSATIONS.filter(
          (eachConversation) => eachConversation.person.toLowerCase().includes(lowerCaseFilter) ||
          eachConversation.caption.toLowerCase().includes(lowerCaseFilter)
        )
      }
      return CONVERSATIONS
    }
    // ---- STATIC DATA END ----
  }
}
</script>

<style lang="scss" scoped>
.vue-whatsapp-layout {
  .whatsapp-sidebar {
    // sidebar css here
    .sidebar-header-wrapper {
      z-index: 2;
      .user-profile-block {
        display: flex;
        align-items: center;

        height: 60px;
        padding: 10px 16px;
        background-color: $grey-dark;
        .status-icon {
          path {
            color: grey;
          }
        }
        .chat-icon, .menu-icon {
          path {
            fill: grey;
          }
        }
      }
      .desktop-notification-block {
        height: 90px;
        padding: 12px 16px;
        background-color: $blue-light;

        display: flex;
        align-items: center;
        .notification-icon {
          outline: none;
          margin-right: 12px;
          path {
            fill: $white;
          }
        }
        .desktop-label-text {
          font-size: 16px;
          line-height: 21px;
          font-weight: 450;
          color: #303030;
          letter-spacing: 0.2px;
        }
        .desktop-action-text {
          font-size: 14px;
          color: #303030;
          cursor: pointer;
          &:hover {
            text-decoration: underline;
          }
        }
      }
      .search-chat-block {
        height: 50px;
        padding: 8px 14px;
        background-color: $grey;
      }
    }
    .all-conversations {
      .conversation-card {
        border-top: 1px solid $grey-dark;
      }
    }
  }
}
</style>

<style lang="scss">
.vue-whatsapp-layout {
  // Here, the css is not scoped. We update the framework css here
  .whatsapp-sidebar {
    .sidebar-header-wrapper {
      .search-chat-block {
        .q-field__control {
          height: 35px;
        }
      }
    }
  }
}
</style>
