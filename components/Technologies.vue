<template>
    <v-row class="justify-center" align="center">
        <v-col v-for="(val, idx) in List" :key="idx" cols="12" sm="6" md="4" lg="3" class="d-flex justify-center">
            <v-card width="100%" max-width="400">
                <v-card-text class="text-center">
                    {{ val }}
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</template>

<script setup>
import { ref } from 'vue'

const List = ref(["hello world", "Gurumurugan","Coding","computer","dfasf"])
</script>