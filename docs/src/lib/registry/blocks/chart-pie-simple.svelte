<script lang="ts">
	import { PieChart } from "layerchart";
	import TrendingUpIcon from "@lucide/svelte/icons/trending-up";
	import * as Chart from "$lib/registry/ui/chart/index.js";
	import * as Card from "$lib/registry/ui/card/index.js";

	const chartData = [
		{ browser: "chrome", visitors: 275, color: "var(--color-chrome)" },
		{ browser: "safari", visitors: 200, color: "var(--color-safari)" },
		{ browser: "firefox", visitors: 187, color: "var(--color-firefox)" },
		{ browser: "edge", visitors: 173, color: "var(--color-edge)" },
		{ browser: "other", visitors: 90, color: "var(--color-other)" },
	];

	const chartConfig = {
		visitors: { label: "Visitors" },
		chrome: { label: "Chrome", color: "var(--chart-1)" },
		safari: { label: "Safari", color: "var(--chart-2)" },
		firefox: { label: "Firefox", color: "var(--chart-3)" },
		edge: { label: "Edge", color: "var(--chart-4)" },
		other: { label: "Other", color: "var(--chart-5)" },
	} satisfies Chart.ChartConfig;
</script>

<Card.Root class="flex flex-col">
	<Card.Header class="items-center">
		<Card.Title>Pie Chart</Card.Title>
		<Card.Description>January - June 2024</Card.Description>
	</Card.Header>
	<Card.Content class="flex-1">
		<Chart.Container config={chartConfig} class="mx-auto aspect-square max-h-[250px]">
			<PieChart
				data={chartData}
				key="browser"
				value="visitors"
				cRange={chartData.map((d) => d.color)}
				c="color"
				props={{
					pie: {
						motion: "tween",
					},
				}}
			>
				{#snippet tooltip()}
					<Chart.Tooltip hideLabel />
				{/snippet}
			</PieChart>
		</Chart.Container>
	</Card.Content>
	<Card.Footer class="flex-col gap-2 text-sm">
		<div class="flex items-center gap-2 font-medium leading-none">
			Trending up by 5.2% this month <TrendingUpIcon class="size-4" />
		</div>
		<div class="text-muted-foreground leading-none">
			Showing total visitors for the last 6 months
		</div>
	</Card.Footer>
</Card.Root>
