<script lang="ts">
	import Counter from './Counter.svelte';

	const INVISIBLE_ASCII: Record<number, string> = {
		0: 'NUL',
		1: 'SOH',
		2: 'STX',
		3: 'ETX',
		4: 'EOT',
		5: 'ENQ',
		6: 'ACK',
		7: 'BEL',
		8: 'BS',
		9: 'HT',
		10: 'LF',
		11: 'VT',
		12: 'FF',
		13: 'CR',
		14: 'SO',
		15: 'SI',
		16: 'DLE',
		17: 'DC1',
		18: 'DC2',
		19: 'DC3',
		20: 'DC4',
		21: 'NAK',
		22: 'SYN',
		23: 'ETB',
		24: 'CAN',
		25: 'EM',
		26: 'SUB',
		27: 'ESC',
		28: 'FS',
		29: 'GS',
		30: 'RS',
		31: 'US',
		32: 'SPACE'
	};

	let value = '';
	$: isInvalid = !value.split('').every((v) => v === '0' || v === '1' || v === '\n');

	$: numbers = value
		.split('\n')
		.map((n) => n)
		.filter(Boolean);

	function dec(value: string) {
		return parseInt(value, 2);
	}

	function ascii(value: string) {
		return String.fromCharCode(dec(value));
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section class="flex justify-center items-center h-full font-mono">
	<div class="flex space-x-10">
		<textarea class="h-full" bind:value />

		<div>
			{#if isInvalid}
				<p>Invalid input</p>
			{:else}
				<table class="max-w-md divide-y divide-gray-300">
					<thead>
						<tr>
							<th
								scope="col"
								class="whitespace-nowrap py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
							>
								Binary
							</th>
							<th
								scope="col"
								class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900"
							>
								Decimal
							</th>
							<th
								scope="col"
								class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900"
							>
								Character
							</th>
							<th
								scope="col"
								class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900"
							>
								ASCII
							</th>
						</tr>
					</thead>
					<tbody class="divide-y divide-gray-200 bg-white">
						{#each numbers as number}
							<tr>
								<td class="whitespace-nowrap py-2 pl-4 pr-3 text-sm text-gray-500 sm:pl-0"
									>{number}</td
								>
								<td class="whitespace-nowrap px-2 py-2 text-sm font-medium text-gray-900"
									>{parseInt(number, 2)}</td
								>
								<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-900"
									>{64 + dec(number) <= 90 ? String.fromCharCode(64 + dec(number)) : 'N/A'}</td
								>
								<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-500"
									>{INVISIBLE_ASCII[dec(number)] ? INVISIBLE_ASCII[dec(number)] : ascii(number)}</td
								>
							</tr>
						{/each}
					</tbody>
				</table>
			{/if}
		</div>
	</div>
</section>

<style>
</style>
