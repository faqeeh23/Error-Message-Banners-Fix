<script setup>
import { computed } from 'vue';
import { Info, CheckCircle, AlertTriangle, XCircle } from 'lucide-vue-next';

const props = defineProps({
  type: { 
    type: String, 
    default: 'info',
    validator: (value) => ['info', 'success', 'warning', 'error'].includes(value)
  }
});

const iconComponent = computed(() => {
  const icons = {
    info: Info,
    success: CheckCircle,
    warning: AlertTriangle,
    error: XCircle
  };
  return icons[props.type];
});
</script>

<template>
  <div 
    :class="['submitty-alert', `alert-${type}`]" 
    role="alert"
    aria-live="polite"
  >
    <!-- Icon Container aligned to start to handle long text wrapping -->
    <div class="alert-icon-wrapper flex items-start mt-1">
      <!-- Accessible Icon with explicit shape variation for colorblindness -->
      <div class="icon-circle flex items-center justify-center rounded-full p-2.5 mr-4 shadow-sm">
        <component :is="iconComponent" class="w-8 h-8 flex-shrink-0" aria-hidden="true" />
      </div>
    </div>
    
    <div class="alert-content flex-grow flex flex-col justify-center">
      <!-- Explicit Textual Prefix for extreme accessibility/colorblind support -->
      <span class="text-xs font-bold uppercase tracking-wider mb-1 alert-type-label">
        {{ type }}
      </span>
      <div class="alert-body text-sm md:text-base leading-relaxed">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<style scoped>
.submitty-alert {
  display: flex;
  align-items: flex-start;
  padding: 1.25rem;
  margin-bottom: 1.25rem;
  border-radius: 12px;
  border-left: 5px solid; 
  backdrop-filter: blur(12px);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.submitty-alert:hover {
  transform: translateY(-2px);
}

.alert-info {
  background-color: rgb(0 114 178 / 8%);
  border-left-color: #0072b2;
  color: #93d6fd;
}

.alert-info .icon-circle {
  background-color: rgb(0 114 178 / 10%);
  color: #0072b2;
}

.alert-success {
  background-color: rgb(0 158 115 / 8%);
  border-left-color: #009e73;
  color: #8fffdf;
}

.alert-success .icon-circle {
  background-color: rgb(0 158 115 / 10%);
  color: #009e73;
}

.alert-warning {
  background-color: rgb(230 159 0 / 8%);
  border-left-color: #d98200;
  color: #ffd587;
}

.alert-warning .icon-circle {
  background-color: rgb(230 159 0 / 10%);
  color: #d98200;
}

.alert-error {
  background-color: rgb(185 28 28 / 8%);
  border-left-color: #991b1b;
  color: #ffa8a8;
}

.alert-error .icon-circle {
  background-color: rgb(213 94 0 / 10%);
  color: #b91c1c;
}


:global([class~="dark"]) .alert-info {
  background-color: rgb(0 114 178 / 15%);
  border-left-color: #56b4e9;
  color: #fff;
}

:global([class~="dark"]) .alert-success {
  background-color: rgb(0 158 115 / 15%);
  border-left-color: #009e73;
  color: #fff;
}

:global([class~="dark"]) .alert-warning {
  background-color: rgb(230 159 0 / 15%);
  border-left-color: #f0e442;
  color: #fff;
}

:global([class~="dark"]) .alert-error {
  background-color: rgb(220 38 38 / 15%);
  border-left-color: #dc2626;
  color: #fff;
}
</style>