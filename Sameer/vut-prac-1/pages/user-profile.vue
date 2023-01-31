<template>
  <v-card max-width="448" class="mx-auto" color="grey-lighten-3">
    <v-layout>
      <v-app-bar
        color="teal-darken-4"
        image="https://picsum.photos/1920/1080?random"
      >
        <template v-slot:image>
          <v-img
            gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
          ></v-img>
        </template>

        <template v-slot:prepend>
          <v-app-bar-nav-icon></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>Instagram</v-app-bar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-heart</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-app-bar>

      <v-main>
        <v-container>
          <v-row>
            <v-col>
              <v-avatar size="120">
                <img :src="profile.profile_picture" />
              </v-avatar>
              <h1>{{ profile.name }}</h1>
              <p>{{ profile.bio }}</p>
              <p>Followers: {{ profile.followers }}</p>
              <p>Following: {{ profile.following }}</p>
              <h2>Posts</h2>
              <v-card v-for="post in profile.posts" :key="post.image_url">
                <v-img :src="post.image_url" />
                <v-card-text>{{ post.caption }}</v-card-text>
                <v-card-text>Likes: {{ post.likes }}</v-card-text>
                <h3>Comments</h3>
                <v-card-text
                  v-for="comment in post.comments"
                  :key="comment.username"
                >
                  {{ comment.username }}: {{ comment.text }}
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-main>
    </v-layout>
  </v-card>
</template>

<script>
import { reactive } from "@vue/composition-api";

export default {
  setup() {
    const profile = reactive({
      username: "john_doe",
      name: "John Doe",
      bio: "Entrepreneur | Traveler | Foodie",
      profile_picture: "data:image/jpeg;base64,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",
      followers: 12345,
      following: 6789,
      posts: [
        {
          image_url: "https://example.com/john_doe/post1.jpg",
          caption: "Exploring the streets of Paris 🇫🇷 #travel #paris",
          likes: 500,
          comments: [
            {
              username: "jane_doe",
              text: "Looks amazing! 😍",
            },
            {
              username: "bob_smith",
              text: "Where's your next destination?",
            },
          ],
        },
        {
          image_url: "https://example.com/john_doe/post2.jpg",
          caption: "Trying the best pizza in town 🍕 #foodie #pizza",
          likes: 300,
          commentss: [
            {
              username: "jane_doe",
              text: "Yum! 🤤",
            },
            {
              username: "bob_smith",
              text: "Where did you get that from?",
            },
          ],
        },
      ],
    });

    return {
      profile,
    };
  },
};
</script>
