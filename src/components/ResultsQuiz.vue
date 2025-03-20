<template>
    <div>
      <h2>You've Completed The Quiz!</h2>
      <p>Your Score: {{ score }} / {{ total }}</p>
      <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    props: ["score", "total"],
}
</script>