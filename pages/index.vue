<script setup>
useHead({
  script: [{ src: 'https://js.pay.jp/v2/pay.js', defer: true }]
})
const payjp = useState()
const card = useState()
const token = useState()

onMounted(() => {
  if (!payjp.value) {
    payjp.value = window.Payjp('*************************')
  }
  const elements = payjp.value.elements()
  elements.create('card')
  card.value = elements.getElement('card')
  card.value.mount('#payjp')
})

const onClick = () => {
  payjp.value.createToken(card.value).then(result => {
    console.log(result)
    token.value = result.id
  }).catch(error => {
    console.log(error)
  })
}
</script>

<template>
    <div>
      <div id="payjp"></div>
      <button @click="onClick">token</button>
      <NuxtLink to="/sample">sample</NuxtLink>
      <div>{{ token }}</div>
    </div>
</template>
