<script lang="ts">
  import {Modal, type ModalSettings} from '@skeletonlabs/skeleton'
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
    //
		const waitOneMillisecondPromise = new Promise((resolve) => {
			setTimeout(() => {
				resolve('Done waiting for 1 millisecond');
			}, 1000);
		});

		waitOneMillisecondPromise.then((result) => {
			modalStore.trigger({
				type: 'alert',
				title: 'Triggered',
				body: `${result}`,
				buttonTextCancel: 'Close'
			});
		});
	}
  
</script>


  <Modal/>
  <button class="btn-icon" on:click={triggerFirstModal}> Click</button>
  
