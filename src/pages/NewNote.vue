<script>
import ContainerDiv from "src/components/ContainerDiv.vue";
import { useLocalNotes } from "src/helper";
import { defineComponent, reactive } from "vue";
import { useRouter } from "vue-router";

export default defineComponent({
  components: { ContainerDiv },
  name: "PageNew",
  setup() {
    const router = useRouter();
    const notes = useLocalNotes();

    const note = reactive({
      title: "",
      description: "",
      content: "",
    });

    const submit = () => {
      notes.value.unshift({
        ...note,
        createdAt: Date.now(),
        updatedAt: Date.now(),
      });

      router.push("/");

      note.title = "";
      note.description = "";
      note.content = "";
    };

    return { note, submit };
  },
});
</script>

<template>
  <q-page padding>
    <ContainerDiv>
      <h3>New Note</h3>
      <form @submit="submit">
        <q-input class="q-mt-sm" outlined label="Title" />
        <q-input class="q-mt-sm" outlined label="Description" />
      </form>
    </ContainerDiv>
  </q-page>
</template>
