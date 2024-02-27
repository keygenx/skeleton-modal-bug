<script lang="ts">
  import {Modal} from '@skeletonlabs/skeleton'
  import { initializeStores, getModalStore } from '@skeletonlabs/skeleton';

  initializeStores();

  const modalStore = getModalStore();

  function triggerFirstModal() {
				modalStore.trigger({
			type: 'confirm',
			title: 'Confirmation',
			body:'Confirm to show second modal',
			response: async (r: string) => {
        triggerSecondModal();
			}
		});
	}

	function triggerSecondModal() {
    //if wait time is longer (1000ms for instance) second modal will be shown
		const waitOneMillisecondPromise = new Promise((resolve) => {
			setTimeout(() => {
				resolve('Done waiting for 1 millisecond');
			}, 1);
		});

		waitOneMillisecondPromise.then((result) => {
			modalStore.trigger({
				type: 'alert',
				title: 'Triggered',
				body: `${result}`
			});
		});
	}
  
</script>
  <Modal/>
  <button class="btn-icon" on:click={triggerFirstModal}>Click to show first modal</button>
  
