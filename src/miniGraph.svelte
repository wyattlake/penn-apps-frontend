<script>
	import { Chart, Card, A, Button, Dropdown, DropdownItem, Popover } from 'flowbite-svelte';

	let options = {
		chart: {
			height: '100%',
			type: 'area',
			fontFamily: 'Inter, sans-serif',
			dropShadow: {
				enabled: false
			},
			toolbar: {
				show: false
			}
		},
		tooltip: {
			enabled: true,
			x: {
				show: false
			},
			style: {
				fontFamily: 'Inter, sans-serif',
				fontSize: '20px',
				fontWeight: '300'
			},
			marker: {
				show: false
			}
		},
		fill: {
			type: ['solid', 'gradient'],
			gradient: {
				opacityFrom: 0.55,
				opacityTo: 0,
				shade: '#1C64F2',
				gradientToColors: ['#1C64F2']
			},
			solid: {
				opacity: [0.35, 1]
			}
		},
		dataLabels: {
			enabled: false
		},
		stroke: {
			width: 4,
			curve: 'straight'
		},
		grid: {
			show: true,
			strokeDashArray: 4,
			padding: {
				left: 20,
				right: 2,
				top: -20
			}
		},
		series: [
			{
				name: 'Competition',
				type: 'line',
				data: [5080, 5100, 5090, 5120, 5132, 5180],
				color: '#F3A0F7'
			},
			{
				name: 'You',
				type: 'area',
				data: [5100, 5130, 5070, 5130, 5080, 5050],
				color: '#95E398'
			}
		],
		legend: {
			show: false
		},
		xaxis: {
			categories: ['Feb', '02 Feb', '03 Feb', '04 Feb', '05 Feb', '06 Feb', '07 Feb'],
			labels: {
				show: true,
				hideOverlappingLabels: true,
				rotate: 0,
				style: {
					fontFamily: 'Inter, sans-serif',
					cssClass: 'text-xs font-normal fill-gray-500 dark:fill-gray-400',
					fontSize: '15px',
					fontWeight: '300'
				}
			},
			tooltip: {
				enabled: false
			},
			axisBorder: {
				show: false
			},
			axisTicks: {
				show: false
			}
		},
		yaxis: {
			show: false,
			labels: {
				style: {
					fontFamily: 'Inter, sans-serif',
					cssClass: 'text-xs font-normal fill-gray-500 dark:fill-gray-400',
					fontSize: '20px',
					fontWeight: '300'
				}
			}
		}
	};
</script>

<Chart {options} />
