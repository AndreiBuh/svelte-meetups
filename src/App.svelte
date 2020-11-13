<script>
  import Header from './UI/Header.svelte';
  import MeetupGrid from './Meetups/MeetupGrid.svelte';
  import EditMeetup from './Meetups/EditMeetup.svelte';
  import TextInput from './UI/TextInput.svelte';
  import Button from './UI/Button.svelte';

  let meetups = [
    {
      id: 'm1',
      title: 'Coding bootcamp',
      subtitle: 'Learn to code in hours',
      description: 'We will have some experts that teach you how to code',
      imageUrl:
        'https://woocommerce.com/wp-content/themes/woo/images/wc-meetups/host-meetup.jpg',
      address: '27th Nerd Road, 43423 New York',
      contactEmail: 'coding@yahoo.com',
      isFavorite: false,
    },
    {
      id: 'm2',
      title: 'Swim together',
      subtitle: 'Learn to swim',
      description: 'We will swim some rounds',
      imageUrl:
        'https://cdn.shopify.com/s/files/1/1109/8836/files/Class_Outline_3_73281a3f-c4c8-4b73-becd-e2b191c812c8_2048x2048.png?v=1557267497',
      address: '44th Meal Road, 78345 Manhattan',
      contactEmail: 'swim@yahoo.com',
      isFavorite: false,
    },
  ];

  let editMode;

  const addMeetup = (e) => {
    const newMeetup = {
      id: Math.random().toString(),
      title: e.detail.title,
      subtitle: e.detail.subtitle,
      address: e.detail.address,
      description: e.detail.description,
      imageUrl: e.detail.imageUrl,
      email: e.detail.email,
    };

    meetups = [newMeetup, ...meetups];
    editMode = null;
  };

  const toggleFavorite = (e) => {
    const id = e.detail;
    const updatedMeetup = { ...meetups.find((meetup) => meetup.id === id) };
    updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
    const meetupIndex = meetups.findIndex((meetup) => meetup.id === id);
    const updatedMeetups = [...meetups];
    updatedMeetups[meetupIndex] = updatedMeetup;
    meetups = updatedMeetups;
  };

  const cancelEdit = () => {
    editMode = null;
  };
</script>

<style>
  main {
    margin-top: 5rem;
  }

  .meetup-controls {
    margin: 1rem;
  }
</style>

<Header />
<main>
  <div class="meetup-controls">
    <Button on:click={() => (editMode = 'add')}>New Meetup</Button>
  </div>
  {#if editMode === 'add'}
    <EditMeetup on:save={addMeetup} on:cancel={cancelEdit} />
  {:else}
    <MeetupGrid {meetups} on:togglefavorite={toggleFavorite} />
  {/if}
</main>
