<script lang="ts">
  import "mathlive";
  import type { MathfieldElement, MathfieldElementAttributes } from "mathlive";
  import { onMount} from "svelte";
  import {on} from "svelte/events"

  type Props = { value?: string } & Partial<MathfieldElementAttributes>;
    type promptsDict = {[key: string]:string}
  let { value = $bindable(), 
        carlo = $bindable(),
        getPromptValue = $bindable(),
        ...rest }: Props = $props();
    carlo = {} as promptsDict;

  const init = (node: MathfieldElement) => {
    onMount(()=>{

    for (let p of node.getPrompts()){
        carlo[p] = "ciao";
        console.log(p);
    }
    })
    $effect(() => {
        if (value) node.value = value;
        //   console.log(value);
        
    });
    $effect(() => {
      return on(node, "input", () => {
        value = node.value;
        for (let p of node.getPrompts()) {
            // console.log(node.getPromptValue(p))
            carlo[p] = node.getPromptValue(p);
            // console.log(carlo);
        }
      });
    });
  };
</script>

<math-field use:init {...rest}></math-field>