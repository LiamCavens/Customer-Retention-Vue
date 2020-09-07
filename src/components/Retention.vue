<template>
  <div class="retention">
    <div class="retention-components">Retention Template</div>
  </div>
</template>

<script>
export default {
  name: "retentionv2",
  components: {},
  props: {},
  data: () => {
    return {};
  },
  methods: {},
};
</script>

<style>
.retention {
  background-color: #00263a;
  color: #e1b77e;
  width: 100%;
  display: flex;
  justify-content: center;
  flex: 1;
}

.retention-components {
  margin: 10px;
  padding: 10px 10px 0 10px;
  width: 350px;
  background-color: white;
  color: #00263a;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  position: relative;
}

.slide-fade-enter-active {
  transition: all 0.8s ease;
  transition-delay: 0.4s;
}
.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter {
  transform: translateX(10px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateX(-10px);
  opacity: 0;
}

.help-transition-leave-active,
.help-transition-enter-active {
  transition: opacity 0.5s ease;
}

.help-transition-enter,
.help-transition-leave-to {
  opacity: 0;
}

.help-transition-enter-to,
.help-transition-leave {
  opacity: 1;
}
</style>
