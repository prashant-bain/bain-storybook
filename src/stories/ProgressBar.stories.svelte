<script module>
  import { defineMeta } from '@storybook/addon-svelte-csf';
  import { ProgressBar } from 'carbon-components-svelte';

  const { Story } = defineMeta({
    title: 'Components/ProgressBar',
    component: ProgressBar,
    tags: ['autodocs'],
    argTypes: {
      /* rendering control to avoid passing undefined */
      valueIsSet: { control: { type: 'boolean' }, name: 'Set value (determinate)' },

      /* ProgressBar props */
      value: { control: { type: 'number' } },
      max: { control: { type: 'number' } },
      size: { control: { type: 'select' }, options: ['sm', 'md'] },
      kind: { control: { type: 'select' }, options: ['default', 'inline', 'indented'] },
      status: { control: { type: 'select' }, options: ['active', 'finished', 'error'] },
      labelText: { control: { type: 'text' } },
      hideLabel: { control: { type: 'boolean' } },
      helperText: { control: { type: 'text' } },
      id: { control: { type: 'text' } }
    },
    args: {
      valueIsSet: true,
      value: 42,
      max: 100,
      size: 'md',
      kind: 'default',
      status: 'active',
      labelText: 'Progress bar label',
      hideLabel: false,
      helperText: 'Optional helper text',
      id: 'progress-bar'
    },
    render: template
  });
</script>

{#snippet template(args)}
  <div style="max-width:720px;">
    {#if args.valueIsSet}
      <ProgressBar
        value={args.value}
        max={args.max}
        size={args.size}
        kind={args.kind}
        status={args.status}
        labelText={args.labelText}
        hideLabel={args.hideLabel}
        helperText={args.helperText}
        id={args.id}
      />
    {:else}
      <ProgressBar
        max={args.max}
        size={args.size}
        kind={args.kind}
        status="active"
        labelText={args.labelText}
        hideLabel={args.hideLabel}
        helperText={args.helperText}
        id={args.id}
      />
    {/if}
  </div>
{/snippet}

<!-- Default (Indeterminate) -->
<Story
  name="Default"
  args={{ valueIsSet: false, labelText: 'Progress bar label', helperText: 'Optional helper text' }}
/>

<!-- Determinate example -->
<Story
  name="Percentage"
  args={{ valueIsSet: true, value: 64, max: 100, labelText: 'Progress', helperText: '64 of 100' }}
/>

<!-- Sizes -->
<Story name="Small" args={{ valueIsSet: true, size: 'sm', value: 30, labelText: 'Small progress' }} />
<Story name="Medium" args={{ valueIsSet: true, size: 'md', value: 30, labelText: 'Medium progress' }} />

<!-- Kinds -->
<Story name="Inline" args={{ valueIsSet: true, kind: 'inline', value: 50, labelText: 'Inline progress' }} />
<Story name="Indented" args={{ valueIsSet: true, kind: 'indented', value: 50, labelText: 'Indented progress' }} />

<!-- Statuses -->
<Story name="Finished" args={{ valueIsSet: true, value: 100, status: 'finished', labelText: 'Completed', helperText: 'Done' }} />
<Story name="Error" args={{ valueIsSet: true, value: 0, status: 'error', labelText: 'Failed', helperText: 'Something went wrong' }} />


<!-- Hide label (visually) -->
<Story name="Hide label" args={{ valueIsSet: true, value: 40, hideLabel: true, helperText: 'Label is visually hidden' }} />
