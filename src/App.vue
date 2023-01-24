<template>
  <div class="row">
    <div class="col s8 offset-s2">
      <div class="card-panel">
        <div>
          <form action="">
            <label for="">Enter Your Secret Message</label>
            <input type="text" class="code" />
            <button class="btn">Create</button>
          </form>
        </div>
      </div>

      <div class="card-panel hidden" id="coded">
        <label>Share This Link With Your Friend</label>
        <input type="text" class="share" />
      </div>

      <div class="card-panel hidden" id="uncoded">
        <label>Your Secret Message</label>
        <h5 class="uncoded"></h5>
        <a href="./index.html">Create Your Own Message</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  mounted() {
    const form = document.querySelector("form");
    const input = document.querySelector(".code");
    const share = document.querySelector(".share");
    const inputMessage = document.querySelector(".card-panel");
    const code = document.querySelector("#coded");

    const uncoded = document.querySelector("#uncoded");
    const { hash } = window.location;
    if (hash) {
      const uncodedMessage = document.querySelector(".uncoded");
      uncodedMessage.innerHTML = atob(hash.replace(/#/g, ""));
      uncoded.classList.remove("hidden");
      inputMessage.classList.add("hidden");
    } else {
      let encryptedMessage;
      form.addEventListener("submit", (event) => {
        event.preventDefault();
        if (hash[0] === "#") {
          const coder = input.value.slice(1);
          encryptedMessage = atob(coder);
          share.value = encryptedMessage;
        } else {
          encryptedMessage = btoa(input.value);
          share.value = `${window.location}#${encryptedMessage}`;
        }

        inputMessage.classList.add("hidden");
        code.classList.remove("hidden");
        share.select();
      });
    }
  },
};
</script>

<style>
.row {
  margin-top: 25vh;
}
.hidden {
  display: none !important;
}
</style>
