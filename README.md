
# Hooks du Cycle de Vie en Vue 3

## 1. `onMounted()`
- **Description** : Enregistre une fonction de rappel qui sera appelée après le montage du composant.
- **Utilisation** : Utilisé pour effectuer des effets de bord nécessitant l'accès au DOM.
- **Exemple** :
  ```vue
  <script setup>
  import { ref, onMounted } from 'vue'

  const el = ref()

  onMounted(() => {
    console.log(el.value) // Accède à l'élément DOM
  })
  </script>

  <template>
    <div ref="el"></div>
  </template>
2. onUpdated()
Description : Appelé après que le composant a mis à jour son arbre du DOM.
Utilisation : Pour accéder au DOM mis à jour après un changement d'état.
##Exemple :
```vue
<script setup>
import { ref, onUpdated } from 'vue'

const count = ref(0)

onUpdated(() => {
  console.log(document.getElementById('count').textContent)
})
</script>

<template>
  <button id="count" @click="count++">{{ count }}</button>
</template>
3. onUnmounted()
Description : Appelé après le démontage du composant.
Utilisation : Pour nettoyer les effets de bord, comme les minuteurs ou les écouteurs d'événements.
##Exemple :
```vue
<script setup>
import { onMounted, onUnmounted } from 'vue'

let intervalId
onMounted(() => {
  intervalId = setInterval(() => {
    console.log('Tick')
  }, 1000)
})

onUnmounted(() => clearInterval(intervalId))
</script>




# Hooks du Cycle de Vie dans Vue 3

## Introduction

Les hooks du cycle de vie dans Vue 3 permettent de gérer efficacement le cycle de vie des composants, facilitant ainsi la création d'applications réactives et performantes. Ce document décrit les principaux hooks disponibles et leur utilisation.

## Hooks

### 1. `onBeforeMount()`
- **Description** : Appelé juste avant le montage du composant.
- **Utilisation** : Pour effectuer des actions avant que le DOM ne soit créé.

### 2. `onBeforeUpdate()`
- **Description** : Appelé juste avant la mise à jour de l'arbre du DOM.
- **Utilisation** : Pour accéder à l'état du DOM avant la mise à jour.

### 3. `onBeforeUnmount()`
- **Description** : Appelé juste avant le démontage de l'instance du composant.
- **Utilisation** : Pour effectuer des actions de nettoyage.

### 4. `onErrorCaptured()`
- **Description** : Appelé lorsqu'une erreur d'un composant descendant est interceptée.
- **Utilisation** : Pour gérer les erreurs et éviter les boucles de rendu infinies.

### 5. `onActivated()` et `onDeactivated()`
- **Description** : Appelés lors de l'activation ou de la désactivation d'un composant dans un arbre mis en cache par `<KeepAlive>`.

### 6. `onServerPrefetch()`
- **Description** : Appelé avant que l'instance du composant ne soit rendue sur le serveur.
- **Utilisation** : Pour effectuer une récupération de données côté serveur.

## Conclusion

Ces hooks permettent de gérer efficacement le cycle de vie des composants dans Vue 3, facilitant ainsi la création d'applications réactives et performantes.
