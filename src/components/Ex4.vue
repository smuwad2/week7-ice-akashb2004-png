<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'

type Post = { id: number; subject: string; entry: string; mood: string }

const posts = ref<Post[]>([])
const editingPost = ref<Post | null>(null)
const isEditing = ref(false)

async function loadPosts() {
  const { data } = await axios.get('http://localhost:3000/posts')
  posts.value = data
}

function startEdit(post: Post) {
  editingPost.value = { ...post }
  isEditing.value = true
}

function cancelEdit() {
  isEditing.value = false
  editingPost.value = null
}

async function saveEdit() {
  if (!editingPost.value) return
  const p = editingPost.value
  const { data: updated } = await axios.put(`http://localhost:3000/posts/${p.id}`, p)
  const idx = posts.value.findIndex(x => x.id === updated.id)
  if (idx !== -1) posts.value[idx] = updated
  isEditing.value = false
  editingPost.value = null
}

onMounted(loadPosts)
</script>

<template>
  <table id="postsTable" class="table">
    <thead>
      <tr>
        <th>Id</th><th>Entry</th><th>Mood</th><th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="p in posts" :key="p.id">
        <td>{{ p.id }}</td>
        <td>{{ p.entry }}</td>
        <td>{{ p.mood }}</td>
        <td>
          <button @click="startEdit(p)">Edit</button>
        </td>
      </tr>
    </tbody>
  </table>

  <div v-if="isEditing" id="editPost" style="margin-top:1rem;">
    <label for="entry">Entry</label>
    <textarea id="entry" v-model="editingPost!.entry"></textarea>

    <label for="mood">Mood</label>
    <select id="mood" v-model="editingPost!.mood">
      <option>Happy</option>
      <option>Sad</option>
      <option>Angry</option>
      <option>Neutral</option>
    </select>

    <div style="margin-top:.5rem;">
      <button @click="saveEdit">Save</button>
      <button @click="cancelEdit">Cancel</button>
    </div>
  </div>
</template>
