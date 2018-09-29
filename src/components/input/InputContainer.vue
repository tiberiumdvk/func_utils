<template>
    <div>
        <div class="input-group" v-for="(func, index) in functions" :key="index">
            <div class="input-group-prepend">
                <span class="input-group-text">&#402;&#x27EE;&#x1d465;&#x27EF; &#61;</span>
            </div>
            <input type="text" class="form-control" v-model.trim="func.fn" @keydown.enter="submit({v: func, i: index})" @keydown.backspace="tryRemove({v: func, i: index})">
        </div>
    </div>
</template>

<script>
export default {
  name: "InputContainer",
  props: {
    functions: {
      type: Array,
      required: true
    },
    onUpdated: {
      type: Function,
      required: true
    }
  },
  methods: {
    submit(sender) {
      try {
        let x;
        eval(sender.v.fn);
        this.onUpdated();
        this.tryAdd(sender);
      }
      catch(e) {
        // TODO: add indicator
      }
    },
    tryAdd(sender) {
      if (sender.v.fn.trim() != "" && sender.i + 1 == this.functions.length) {
        this.functions.push({ fn: "" });
      }
      
      this.onUpdated();
    },
    tryRemove(sender) {
      if (sender.v.fn.length < 1 && this.functions.length > 1) {
        this.functions = this.functions.filter(v => v != sender.v);
        this.onUpdated();
      }
    }
  }
};
</script>

<style>
div.input-group {
  margin: 20px auto !important;
}
</style>
