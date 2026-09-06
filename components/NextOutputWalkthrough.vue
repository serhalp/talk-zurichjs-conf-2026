<script setup lang="ts">
import { ref } from "vue";

const stage = ref<HTMLElement>();
let label: HTMLSpanElement | undefined;
let origin: { x: number; y: number } | undefined;

function position(element: Element) {
  const bounds = element.getBoundingClientRect();
  const parent = stage.value!.getBoundingClientRect();
  const scale = parent.width / stage.value!.offsetWidth;
  return {
    x: (bounds.left - parent.left) / scale,
    y: (bounds.top - parent.top) / scale,
  };
}

function beforeLeave(element: Element) {
  label?.remove();
  label = undefined;
  const source = element.querySelector<SVGTextElement>(".next-label");
  if (!source || matchMedia("(prefers-reduced-motion: reduce)").matches) return;

  origin = position(source);
  label = document.createElement("span");
  label.textContent = ".next/";
  label.className = "travelling-directory";
  Object.assign(label.style, {
    left: `${origin.x}px`,
    top: `${origin.y}px`,
  });
  stage.value!.append(label);
  source.style.visibility = "hidden";
}

function enter(element: Element) {
  if (!label || !origin) return;
  const target = element.querySelector<HTMLElement>("code .line");
  if (!target) {
    label.remove();
    label = undefined;
    return;
  }

  const destination = position(target);
  const movingLabel = label;
  element.classList.add("directory-arriving");
  target.style.visibility = "hidden";
  const animation = movingLabel.animate(
    [
      { transform: "translate(0, 0)", fontSize: "20px" },
      {
        transform: `translate(${destination.x - origin.x}px, ${destination.y - origin.y}px)`,
        fontSize: getComputedStyle(target).fontSize,
      },
    ],
    {
      duration: 850,
      easing: "cubic-bezier(0.22, 1, 0.36, 1)",
      fill: "forwards",
    },
  );
  animation.finished.then(() => {
    target.style.visibility = "";
    element.classList.remove("directory-arriving");
    movingLabel.remove();
    if (label === movingLabel) label = undefined;
  });
}
</script>

<template>
  <div ref="stage" class="walkthrough">
    <Transition
      name="manifest-step"
      mode="out-in"
      @before-leave="beforeLeave"
      @enter="enter"
    >
      <slot />
    </Transition>
  </div>
</template>

<style scoped>
.walkthrough {
  position: relative;
}
.walkthrough :deep(.directory-arriving) {
  animation: directory-reveal 300ms 550ms ease both;
}
@keyframes directory-reveal {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.walkthrough :deep(.travelling-directory) {
  position: absolute;
  z-index: 5;
  font-family: var(--slidev-code-font-family);
  font-size: 20px;
  line-height: 1;
  color: #f8fafc;
  pointer-events: none;
}
</style>
