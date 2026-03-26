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
  border-left-width: 5px;
  border-left-style: solid;
  /* Premium Glassmorphism & Depth */
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

/* Hover elevation effect */
.submitty-alert:hover {
  transform: translateY(-2px);
}

.alert-info {
  background-color: rgba(0, 114, 178, 0.08);
  border-left-color: #0072B2;
  color: #048fe0;
}
.alert-info .icon-circle {
  background-color: rgba(0, 114, 178, 0.1);
  color: #0072B2;
}
.alert-info .alert-type-label { color: #0072B2; }

.alert-success {
  background-color: rgba(0, 158, 115, 0.08);
  border-left-color: #009E73;
  color: #029e72;
}
.alert-success .icon-circle {
  background-color: rgba(0, 158, 115, 0.1);
  color: #009E73;
}
.alert-success .alert-type-label { color: #009E73; }

.alert-warning {
  background-color: rgba(230, 159, 0, 0.08);
  border-left-color: #d98200;
  color: #de9204;
}
.alert-warning .icon-circle {
  background-color: rgba(230, 159, 0, 0.1);
  color: #d98200;
}
.alert-warning .alert-type-label { color: #d98200; }

.alert-error {
  background-color: rgba(185, 28, 28, 0.08);
  border-left-color: #991b1b;
  color: #ea0202;
}
.alert-error .icon-circle {
  background-color: rgba(213, 94, 0, 0.1);
  color: #b91c1c;
}
.alert-error .alert-type-label { color: #b91c1c; }
/* Dark Mode Overrides (High Contrast) */
:global([class~="dark"]) .alert-info {
  background-color: rgba(0, 114, 178, 0.15);
  border-left-color: #56B4E9;
  color: #ffffff;
}
:global([class~="dark"]) .alert-info .icon-circle {
  color: #56B4E9;
}
:global([class~="dark"]) .alert-info .alert-type-label {
  color: #56B4E9;
}

:global([class~="dark"]) .alert-success {
  background-color: rgba(0, 158, 115, 0.15);
  border-left-color: #009E73;
  color: #ffffff;
}
:global([class~="dark"]) .alert-success .icon-circle {
  color: #4ade80;
}
:global([class~="dark"]) .alert-success .alert-type-label {
  color: #4ade80;
}

:global([class~="dark"]) .alert-warning {
  background-color: rgba(230, 159, 0, 0.15);
  border-left-color: #F0E442;
  color: #ffffff;
}
:global([class~="dark"]) .alert-warning .icon-circle {
  color: #F0E442;
}
:global([class~="dark"]) .alert-warning .alert-type-label {
  color: #F0E442;
}

:global([class~="dark"]) .alert-error {
  background-color: rgba(220, 38, 38, 0.15);
  border-left-color: #dc2626;
  color: #ffffff;
}
:global([class~="dark"]) .alert-error .icon-circle {
  color: #ef4444;
}
:global([class~="dark"]) .alert-error .alert-type-label {
  color: #ef4444;
}
</style>
