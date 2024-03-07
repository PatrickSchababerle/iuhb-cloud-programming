<template>
	<!-- Modal -->
	<div class="modal fade" id="disclaimer" data-bs-keyboard="false" tabindex="-1" aria-hidden="true">
		<div class="modal-dialog modal-dialog-centered">
			<div class="modal-content">
				<div class="modal-body text-start py-3">
					<h3>
						Disclaimer
					</h3>
					<p class="mt-3 p-0">
						This website is part of a course of study. The website has no claim to completeness or full functionality and is only used for demonstration purposes. No personal data is processed or stored, the entries made are not passed on to third parties and are stored in the local storage of your browser (localStorage). Responsible for it's content:
					</p>
					<p class="p-0">
						Patrick Schababerle<br>
						Softwareentwicklung (B.Sc.)<br>
						IU International University of Applied Sciences
					</p>
					<p class="mb-5 p-0">
						By using this site you agree to these conditions.
					</p>
					<button class="btn btn-primary w-100" data-bs-dismiss="modal" @click="this.disclaimerConfirmed()">
						Continue
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'DisclaimerModal',
	methods: {

		disclaimerConfirmed() {
			localStorage.setItem('disclaimer_confirmed', "1");
		}

	}
}
</script>

<style>
	.modal-content {
		border-radius: 15px !important;
	}
	.modal-body {
		border-radius: 13px;
		background-color: var(--background-color);
	}
</style>