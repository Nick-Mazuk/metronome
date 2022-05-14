<script lang="ts">
    import Button from '@nick-mazuk/ui-svelte/src/elements/button/button.svelte'
    import PauseIcon from '@nick-mazuk/ui-svelte/src/elements/icon/pause.svelte'
    import PlayIcon from '@nick-mazuk/ui-svelte/src/elements/icon/play.svelte'
    import FormEntity from '@nick-mazuk/ui-svelte/src/form/form-entity/form-entity.svelte'
    import NumberInput from '@nick-mazuk/ui-svelte/src/form/inputs/number-input/number-input.svelte'
    import Select from '@nick-mazuk/ui-svelte/src/form/inputs/select/select.svelte'
    const defaultPercentage = 0.9
    const defaultTempo = 120
    type Difficulty = {
        name: string
        percentage: number
    }
    let metronomePercentage = defaultPercentage
    const difficulties: Difficulty[] = [
        {
            name: 'Easy',
            percentage: defaultPercentage,
        },
        {
            name: 'Medium',
            percentage: 0.75,
        },
        {
            name: 'Hard',
            percentage: 0.5,
        },
        {
            name: 'Extreme',
            percentage: 0.25,
        },
    ]

    const buttonProps = {
        play: {
            text: 'Play',
            icon: PlayIcon,
        },
        pause: {
            text: 'Pause',
            icon: PauseIcon,
        },
    } as const

    let isPlaying = false
    let interval: ReturnType<typeof setInterval> | undefined
    let tempo = 120

    const handleSubmit = async () => true

    $: {
        if (interval) window.clearInterval(interval)
        if (isPlaying) {
            let tickCount = 0
            interval = setInterval(() => {
                if (tickCount < 5 || Math.random() < metronomePercentage) {
                    new Audio('/metronome.wav').play()
                }
                tickCount++
            }, 60_000 / tempo)
        }
    }
</script>

<FormEntity title="Settings" handleSubmit="{handleSubmit}" primaryAction="" secondaryAction="">
    <svelte:fragment slot="extra-actions">
        <Button
            variant="primary"
            size="small"
            prefix="{buttonProps[isPlaying ? 'pause' : 'play'].icon}"
            on:click="{() => (isPlaying = !isPlaying)}"
        >
            {buttonProps[isPlaying ? 'pause' : 'play'].text}
        </Button>
    </svelte:fragment>
    <div class="form-layout-horizontal">
        <NumberInput
            label="Tempo (BPM)"
            optional
            hideOptionalLabel
            on:change="{(event) =>
                (tempo = isNaN(event.detail.parsedValue)
                    ? defaultTempo
                    : event.detail.parsedValue)}"
            placeholder="{String(defaultTempo)}"
            defaultValue="{String(defaultTempo)}"
            disallowNegatives
            decimals="{0}"
            max="{999}"
            min="{1}"
        />
        <Select
            label="Difficulty"
            defaultValue="{'defaultPercentage'}"
            on:change="{(event) => (metronomePercentage = parseFloat(event.detail))}"
        >
            {#each difficulties as { name, percentage }}
                <option value="{percentage}">{name} ({percentage * 100}%)</option>
            {/each}
        </Select>
    </div>
</FormEntity>
