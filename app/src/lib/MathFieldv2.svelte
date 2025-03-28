<script lang="ts">
  import "mathlive";
  import type { MathfieldElement, MathfieldElementAttributes } from "mathlive";
  import { onMount} from "svelte";
  import {on} from "svelte/events"
  import "mathlive/fonts.css"
  
  export type promptsDict = {[key: string]:string}
  type Props = { value?: string, prompts?:promptsDict } & Partial<MathfieldElementAttributes>;
  let { value = $bindable(), 
        prompts = $bindable(),
        getPromptValue = $bindable(),
        ...rest }: Props = $props();

  prompts = {};
  const init = (node: MathfieldElement) => {
    onMount(()=>{
        node.smartFence = true;
        for (let p of node.getPrompts()){
            console.log(p);
        }
    })
    $effect(() => {
        if (value) node.value = value;
        if (prompts) {
            for (let p in prompts) {
                if (node.getPromptValue(p) != prompts[p]){
                    node.setPromptValue(p, prompts[p], {})
                }
            }
        } 
    });
    $effect(() => {
      return on(node, "input", () => {
        value = node.value;
        for (let p of node.getPrompts()) {
            prompts[p] = node.getPromptValue(p);
        }
      });
    });
  };
</script>

<math-field use:init {...rest}></math-field>

<style>
    math-field::part(virtual-keyboard-toggle) {
        display: none;
    }
    math-field::part(menu-toggle) {
        display: none;
    }
    math-field::part(placeholder) {
        border: none;
        background-color: red;
    }
</style>