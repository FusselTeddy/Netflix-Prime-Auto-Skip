<script setup lang="ts">
import { Notivue, Notification } from "notivue"
const isFirefox = typeof browser !== "undefined"
const version = __VERSION__
const githubUrl = __GITHUB_URL__
import { useFrontendStore } from "@/stores/options.store"
// wont sync without opening once
useFrontendStore()
const router = useRouter()
const hash = ref(router.currentRoute.value.path)
// watch router route changed
watch(
	() => router.currentRoute.value.path,
	(newHash) => {
		console.log(newHash)
		hash.value = newHash
	},
	{
		immediate: true,
		deep: true,
	},
)
</script>
<template>
	<div
		class="wrapper"
		style="height: calc(min(100vh, 1800px))"
	>
		<div class="sidenav flex flex-col">
			<div class="flex justify-center items-center flex-col IconBox">
				<div class="flex justify-center items-center flex-row">
					<img
						class="Logo"
						src="@/assets/Logo/NetflixAmazon Auto-Skip.svg"
						alt="Logo"
					/>
					<div class="flex justify-center items-center flex-col">
						<h2 class="title">
							{{ $t("pageTitle") }}
						</h2>
						<p class="font text-base text-white">{{ version }}</p>
					</div>
				</div>
				<a
					target="_blank"
					class="flex justify-center items-center flex-col text-center no-underline"
					:href="
						isFirefox
							? 'https://addons.mozilla.org/firefox/addon/netflix-prime-auto-skip/'
							: 'https://chrome.google.com/webstore/detail/netflixprime-auto-skip/akaimhgappllmlkadblbdknhbfghdgle'
					"
				>
					<p class="text-base text-white">
						{{ $t("rateNow") }}
					</p>
					<img
						:src="
							isFirefox
								? 'https://img.shields.io/amo/stars/NetflixPrime@Autoskip.io?color=e60010'
								: 'https://img.shields.io/chrome-web-store/stars/akaimhgappllmlkadblbdknhbfghdgle?color=e60010'
						"
						alt="rating"
						class="w-24"
					/>
				</a>
			</div>
			<div class="flex flex-col MenuButtons flex-wrap">
				<RouterLink
					to="/options-page/SharedSettings"
					class="menuButton flex"
					:class="hash.endsWith('SharedSettings') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<i-mdi-transit-connection-variant class="icon" />
					<div>
						{{ $t("sharedSettings") }}
					</div>
				</RouterLink>
				<RouterLink
					to="/options-page/Amazon"
					class="menuButton flex"
					:class="hash.endsWith('Amazon') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 24 24"
						class="icon text-primary-content"
					>
						<path
							fill="currentColor"
							d="M13.2,11H10V7H13.2A2,2 0 0,1 15.2,9A2,2 0 0,1 13.2,11M13,3H6V21H10V15H13A6,6 0 0,0 19,9C19,5.68 16.31,3 13,3Z"
						/>
					</svg>
					<div>Prime Video</div>
				</RouterLink>
				<RouterLink
					to="/options-page/Netflix"
					class="menuButton flex"
					:class="hash.endsWith('Netflix') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<i-mdi-netflix class="icon" />
					<div>Netflix</div>
				</RouterLink>
				<RouterLink
					to="/options-page/Disney"
					class="menuButton flex"
					:class="hash.endsWith('Disney') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<svg
						preserveAspectRatio="xMidYMid meet"
						viewBox="0 0 700 700"
						width="700pt"
						xmlns="http://www.w3.org/2000/svg"
						class="icon text-primary-content"
					>
						<!-- fill="#1d1fff" -->
						<path
							transform="matrix(.1 0 0 -.1 0 700)"
							fill="currentColor"
							d="m1457 6123c-1-1-52-4-112-7-61-4-123-8-140-11-16-2-55-7-85-10s-66-7-80-10c-14-2-56-9-95-15-120-19-295-59-410-94-60-19-143-44-184-56-65-19-82-29-130-79-56-57-149-188-193-271-28-55-30-141-4-186 45-76 192-120 373-112 142 7 224 30 247 69 16 28 16 32 2 54-9 14-23 25-31 25-9 0-23 4-33 10-18 10-167 54-220 65-77 16-5 60 161 100 56 13 119 26 141 30 21 3 41 7 45 9 3 2 33 7 66 11s74 8 90 10c201 25 714 25 880 0 30-4 94-11 190-21 28-3 75-9 105-14s71-12 90-15c46-7 138-24 170-30 14-3 39-8 55-11 213-38 604-144 865-233 137-46 408-152 540-211 135-59 519-250 620-308 47-26 105-60 130-74 158-89 518-331 650-435 30-25 62-50 70-56 132-105 202-169 360-327 380-380 604-777 648-1150 8-72 8-229-1-307-17-140-84-317-172-455-84-129-266-293-450-405-83-50-417-196-472-206-10-2-51-14-92-26-41-13-81-24-90-27-104-25-203-46-272-58-123-22-138-24-204-31-33-3-80-9-105-13-63-9-467-8-575 1-129 12-144 13-205 22-30 4-66 9-80 10-69 8-236 38-242 43-10 10-27 638-33 1207l-3 361 78-2c111-2 398-15 440-19 19-2 67-6 105-10 39-3 81-8 95-10s49-7 79-10c30-4 63-9 75-11s39-6 62-9c35-4 150-25 209-39 242-54 358-100 433-173 41-39 44-45 39-79-9-55-65-106-176-160-162-79-191-110-142-151 31-27 163-76 249-93 140-28 284 29 414 163 91 94 138 207 143 344 4 104-11 163-72 277-24 45-170 187-238 231-152 99-392 195-579 231-12 2-55 11-96 19s-92 17-114 20c-21 2-46 7-55 9-9 3-101 17-206 32-153 21-241 27-449 30-142 2-260 5-262 7-1 1-5 65-8 142-6 137-13 234-21 305-2 19-7 62-10 95-9 91-35 236-56 315-25 92-166 292-224 316-67 28-107-17-154-173-28-95-65-285-76-388-3-27-7-66-10-85-14-109-22-191-31-330-4-58-8-121-9-140-2-19-3-54-4-76l-1-42-67-13c-38-7-70-14-73-14-3-1-23-5-45-9-162-31-516-137-705-211-222-87-497-239-586-324-112-106-163-212-165-338-2-91 37-198 96-265 11-13 31-39 45-58 148-213 490-541 780-746 182-129 419-271 601-358 75-37 75-37 77-79 2-23 5-49 7-57s7-35 10-59c11-76 53-230 78-284 27-58 81-118 130-144 24-14 54-18 122-18 80 1 97 4 155 33 36 17 72 37 81 44 33 27 61 144 63 266 0 27 18 28 96 7 30-8 80-19 110-25s66-12 80-15c32-7 200-32 265-40 28-4 60-8 72-10 59-9 278-19 438-19 165 0 391 10 404 19 3 1 35 6 71 9 54 6 275 44 345 60 426 98 843 286 1120 504 106 84 262 247 337 353 151 212 265 507 294 760 3 30 9 77 13 104 17 117 3 283-36 449-132 558-540 1144-1154 1656-118 99-252 201-371 283-167 115-201 138-333 218-358 220-679 384-975 499-30 12-68 28-85 35-91 41-461 167-674 229-328 97-756 187-1051 221-25 3-61 7-80 10-42 5-128 12-265 21-90 6-434 12-438 7zm1199-3632c-4-207-9-403-11-436s-6-109-9-170c-12-207-25-387-29-391-1-1-49 17-107 40-382 155-699 343-975 580-89 76-245 232-272 271-42 60-33 141 20 188 56 50 328 144 532 183 11 2 31 6 45 9 56 12 175 33 225 39 11 2 38 6 60 10s56 8 75 10c57 6 153 17 180 21 14 2 66 7 115 10 50 4 91 8 92 9 1 0 16 2 33 2l32 2z"
						/>
					</svg>
					<div>Disney+</div>
				</RouterLink>
				<RouterLink
					to="/options-page/Crunchyroll"
					class="menuButton flex"
					:class="hash.endsWith('Crunchyroll') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<svg
						viewBox="1.8 1.581 247.263 220"
						xmlns="http://www.w3.org/2000/svg"
						class="icon text-primary-content"
					>
						<g>
							<path
								fill="currentColor"
								d="m115.377 209.8c-3.54-.33-12.852-1.943-16.306-2.825-29.863-7.625-55.154-28.074-68.537-55.418-7.337-14.99-10.395-28.396-10.383-45.52.012-17.144 3.117-30.818 10.335-45.52 5.406-11.01 11.625-19.636 20.453-28.37 16.513-16.336 37.43-26.45 61.124-29.552 7.746-1.014 24.143-.684 31.377.631 15.045 2.737 28.553 8.112 40.658 16.178 25.149 16.76 41.461 42.39 45.714 71.828.91 6.303 1.437 19.42.824 20.515-.335.598-.508-.028-.727-2.62-1.086-12.843-6.642-28.373-14.307-39.991-23.298-35.313-66.767-50.295-107.013-36.883-31.064 10.352-54.41 36.615-60.818 68.416-3.169 15.725-2.218 31.139 2.86 46.355 8.953 26.836 30.382 48.274 57.558 57.584 6.41 2.196 14.64 4.026 20.068 4.461 6.5.522 4.861 1.018-3.157.956-4.376-.033-8.75-.135-9.723-.225z"
							/>
							<path
								fill="currentColor"
								d="m137.695 196.826c-33.594-2.447-61.427-27.495-67.236-60.507-1.057-6.008-1.261-17.24-.413-22.769 5.036-32.827 30.288-57.733 63.23-62.362 6.676-.938 18.574-.61 24.969.69 5.562 1.13 11.728 3.138 16.572 5.394l3.757 1.75-3.536 1.669c-12.758 6.025-20.633 20.118-18.784 33.619 1.851 13.52 11.2 24.13 24.622 27.945 4.832 1.374 12.22 1.373 17.054 0 6.25-1.777 11.152-4.682 15.613-9.254 1.506-1.544 2.835-2.648 2.954-2.455.119.194.463 2.322.765 4.73.745 5.939.308 17.238-.886 22.88-3.803 17.967-13.386 33.049-28.08 44.192-13.907 10.546-32.305 15.81-50.601 14.478z"
							/>
						</g>
					</svg>
					<div>Crunchyroll</div>
				</RouterLink>
				<RouterLink
					to="/options-page/Backup"
					class="menuButton flex"
					:class="hash.endsWith('Backup') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<i-mdi-dots-horizontal class="icon" />
					<p>{{ $t("backup") }}</p>
				</RouterLink>
				<RouterLink
					to="/options-page/Statistics"
					class="menuButton flex"
					:class="hash.endsWith('Statistics') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<i-mdi-chart-bar class="icon" />
					<p>{{ $t("statistics") }}</p>
				</RouterLink>
				<RouterLink
					to="/options-page/Changelog"
					class="menuButton flex"
					:class="hash.endsWith('Changelog') ? 'bg-netflix' : 'bg-primary'"
					draggable="false"
				>
					<i-mdi-format-list-bulleted class="icon" />
					<p>{{ $t("changelog") }}</p>
				</RouterLink>
			</div>
			<div class="mt-auto">
				<div class="flex flex-col mb-2 MenuButtons">
					<a
						class="btn btn-secondary rounded-2xl blueButtons m-[5px_15px]"
						:href="githubUrl"
						target="_blank"
					>
						<i-mdi-github class="icon" />
						Github
					</a>
					<a
						class="btn btn-secondary rounded-2xl blueButtons m-[5px_15px]"
						href="https://github.com/sponsors/Dreamlinerm"
						target="_blank"
					>
						<i-mdi-gift
							height="2rem"
							width="2rem"
						/>
						{{ $t("donate") }}
					</a>
				</div>
			</div>
		</div>
		<div class="content flex flex-col overflow-y-auto w-full">
			<div class="page">
				<div class="p-4 prose">
					<RouterView />
				</div>

				<Notivue v-slot="item">
					<Notification :item="item" />
				</Notivue>
			</div>
		</div>
	</div>
</template>

<style scoped>
/* The side navigation menu */
.sidenav {
	@apply h-full bg-[#111] px-2.5 gap-5;
}
.menuButton {
	@apply rounded-[15px] m-[5px_15px] p-[13px_20px] max-w-[400px] no-underline whitespace-nowrap cursor-pointer text-primary-content text-[1.5rem] select-none items-center;
	/*TODO: change whitespace according language*/
}
/* When you mouse over the navigation links, change their color */
.menuButton:hover {
	background-color: #4d0000;
}
.IconBox {
	@apply p-5;
}
.Logo {
	@apply h-12;
}
.title {
	@apply py-0 text-white;
}

.content {
	@apply min-w-[200px] min-h-[450px];
}
.page {
	@apply p-[80px_0_0_3%] w-[97%];
}

.icon {
	@apply w-8 h-8 mx-1.5;
}
.wrapper {
	@apply flex flex-row;
}

@media only screen and (max-width: 800px), only screen and (max-height: 600px) {
	.wrapper {
		@apply flex flex-col;
	}
	.menuButton p,
	.menuButton div,
	.IconBox {
		@apply hidden;
	}
	.MenuButtons {
		@apply pt-1.5;
	}
}

@media only screen and (max-height: 800px), only screen and (max-width: 1000px) {
	.wrapper {
		@apply flex flex-col;
	}
	.MenuButtons {
		@apply flex-row justify-center;
	}
	.menuButton {
		@apply m-1.5 px-2.5 py-1.5;
	}
	.blueButtons {
		@apply mx-1.5 text-base !important;
	}
	body {
		@apply flex-col;
	}
	.page {
		@apply p-0 mx-3.5 w-[calc(100%-30px)];
	}
	.IconBox {
		@apply pt-2.5 flex-row;
	}
	.sidenav {
		@apply h-auto block;
	}
}
</style>
