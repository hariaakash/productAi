<script>
	import Sidebar from "$lib/components/sidebar.svelte";

    let content = '';
    let includeGuide = '';
    let excludeGuide = '';
    /**
	 * @type {any[]}
	 */
    let messages = [
        // { sender: 'user', content: 'Hello!' },
        // { sender: 'assistant', content: 'Hi there! How can I assist you today?' },
        // { sender: 'user', content: 'Can you help me with a coding problem?' },
        // { sender: 'assistant', content: 'Sure, please provide more details about the problem.' },
        // { sender: 'user', content: 'Hello!' },
        // { sender: 'assistant', content: 'Hi there! How can I assist you today?' },
        // { sender: 'user', content: 'Can you help me with a coding problem?' },
        // { sender: 'assistant', content: 'Sure, please provide more details about the problem.' },
        // { sender: 'user', content: 'Hello!' },
        // { sender: 'assistant', content: 'Hi there! How can I assist you today?' },
        // { sender: 'user', content: 'Can you help me with a coding problem?' },
        // { sender: 'assistant', content: 'Sure, please provide more details about the problem.' },
    ];
    const handleSubmit = () => {
        messages.push({
            sender: 'user',
            content,
        });
        messages.push({
            sender: 'assistant',
            content: 'Sure, please provide more details about the problem.',
        });
        messages = messages;
        console.log(messages);
        content = '';
    };
</script>

<!-- Container -->
<div class="bg-black text-white h-screen flex flex-col mx-2">
    <div class="p-4 flex-grow-0 h-1/5">
      <!-- Top area -->
    </div>
  
    <div class="flex-grow h-4/5 flex">
      <div class="w-2/3 pr-4">
        <!-- Main content area (Chat) -->
        <div class="bg-gray-800 p-4 rounded h-full overflow-y-auto flex flex-col-reverse">
          <div class="space-y-4">
            <!-- Chat messages -->
            {#each messages as message}
              <div class:text-right={message.sender === 'user'} class="flex items-start">
                <div
                  class:bg-blue-500={message.sender === 'user'}
                  class:ml-auto={message.sender === 'user'}
                  class:bg-gray-700={message.sender === 'assistant'}
                  class:mr-auto={message.sender === 'assistant'}
                  class="p-2 mx-4 rounded-lg max-w-xs text-white flex items-center justify-between w-1/3"
                >
                  <span>{message.content}</span>
                  <img
                    src={message.sender === 'user' ? '/user.png' : '/robot.jpg'}
                    alt="User"
                    class="w-8 h-8 rounded-full ml-2"
                    class:order-first={message.sender === 'user'}
                  />
                </div>
              </div>
            {/each}
          </div>
        </div>
      </div>
  
      <div class="w-1/3 bg-gray-800 p-4 rounded">
        <!-- Sidebar content -->
        <Sidebar />
      </div>
    </div>
  
    <!-- Input -->
    <div class="bg-gray-800 p-2 my-2 rounded flex items-center">
      <form on:submit|preventDefault={handleSubmit} class="flex items-center justify-between w-full">
        <input
          class="bg-transparent text-white placeholder-gray-500 flex-1 outline-none"
          type="text"
          placeholder="How Can I Help You ?"
          bind:value={content}
        />
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" type="submit">
          Submit
        </button>
      </form>
    </div>
  </div>