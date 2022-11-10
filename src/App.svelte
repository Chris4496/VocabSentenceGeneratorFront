<script>
  let words = [];
  let n = 1;

  let textarea = "";

  let loading = false;

  const apiurl = "https://generator-api-gtolrvmqsq-uc.a.run.app";

  // seperate by new line
  $: words = textarea.split(/\r?\n/);

  // fetch the file and blob
  async function fetch_text_file() {
    let params = new URLSearchParams();
    words.forEach((word) => params.append("q", word));
    params.append("n", n.toString());

    fetch(apiurl + "/getSentences/textFile?" + params.toString())
      .then((response) => response.blob())
      .then((blob) => {
        console.log(blob);
        // create a new blob url reference to the file
        const url = URL.createObjectURL(blob);
        // download the file
        const a = document.createElement("a");
        a.href = url;
        a.download = "exercise.txt";
        document.body.appendChild(a); // we need to append the element to the dom -> otherwise it will not work in firefox
        a.click();
        a.remove(); //afterwards we remove the element again
      });
  }

  async function fetch_docx_file() {
    let params = new URLSearchParams();
    words.forEach((word) => params.append("q", word));
    params.append("n", n.toString());

    fetch(apiurl + "/getSentences/docxFile?" + params.toString())
      .then((response) => response.blob())
      .then((blob) => {
        console.log(blob);
        // create a new blob url reference to the file
        const url = URL.createObjectURL(blob);

        // download the file
        const a = document.createElement("a");
        a.href = url;
        a.download = "exercise.docx";
        document.body.appendChild(a); // we need to append the element to the dom -> otherwise it will not work in firefox
        a.click();
        a.remove(); //afterwards we remove the element again
      });
  }

  async function fetch_pdf_file() {
    let params = new URLSearchParams();
    words.forEach((word) => params.append("q", word));
    params.append("n", n.toString());

    fetch(apiurl + "/getSentences/pdfFile?" + params.toString())
      .then((response) => response.blob())
      .then((blob) => {
        console.log(blob);
        // create a new blob url reference to the file
        const url = URL.createObjectURL(blob);

        // download the file
        const a = document.createElement("a");
        a.href = url;
        a.download = "exercise.pdf";
        document.body.appendChild(a); // we need to append the element to the dom -> otherwise it will not work in firefox
        a.click();
        a.remove(); //afterwards we remove the element again
      });
  }

  async function fetch_handler(type) {
    // check if the textarea is empty
    if (textarea === "") {
      alert("Please enter some words");
      return;
    }
    loading = true;
    switch (type) {
      case "textFile":
        await fetch_text_file();
        break;
      case "docxFile":
        await fetch_docx_file();
        break;
      case "pdfFile":
        await fetch_pdf_file();
        break;
      default:
        break;
    }
  }
</script>

<main>
  <div class="relative bg-white">
    <div class="mx-auto max-w-7xl px-4 sm:px-6">
      <div
        class="flex items-center justify-between border-b-2 border-gray-100 py-6 md:justify-start md:space-x-10"
      >
        <div class="flex justify-start lg:w-0 lg:flex-1">
          <h1 class="font-sans font-bold text-2xl text-gray-700 tracking-wide">
            Vocab Exercise Generator
          </h1>
        </div>
        <div class="items-center justify-end md:flex md:flex-1 lg:w-0">
          <a
            as="button"
            target="_blank"
            rel="noopener noreferrer"
            href="https://github.com/Chris4496/VocabSentenceGeneratorFront"
            class="whitespace-nowrap text-base font-medium text-gray-500 hover:text-gray-900"
            >View Code</a
          >
        </div>
      </div>
    </div>
  </div>
  <div class="relative bg-white">
    <div class="mt-20 px-7 mx-auto max-w-6xl">
      <div class="flex flex-row flex-wrap h-full md:divide-y-0 divide-y-2">
        <div class="md:basis-1/2 w-full">
          <p class="font-sans font-bold text-5xl lg:mb-4">Create Your Own</p>
          <p class="font-sans font-bold text-5xl">
            <span
              class="font-bold underline underline-offset-4 decoration-sky-500"
              >Vocabulary</span
            >
            Exercise!
          </p>
          <h1 class="font-sans font-bold text-xl my-7">Example:</h1>
          <div
            class="p-2.5 h-32 w-full md:w-5/6 text-md text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 my-2 font-sans"
          >
            hello <br /> world <br /> example
          </div>
          <!-- arrow pointing down -->
          <div class="flex justify-center w-full md:w-5/6">
            <svg
              class="w-6 h-6 text-gray-500"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 14l-7 7m0 0l-7-7m7 7V3"
              />
            </svg>
          </div>
          <div
            class="p-2.5 h-46 w-full md:w-5/6 text-md text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 my-2 font-sans"
          >
            1. Say _____ to Liz for me. <br /> 2. the major _____ religions
            <br /> 3. Let me give you an _______ of what I mean. <br />
            -------------------- <br />
            Answers: <br /> 1. hello | 2. world | 3. example
          </div>
        </div>
        <div class="md:basis-1/2 w-full">
          <h3 class="font-sans font-bold text-xl">Enter words here:</h3>
          <textarea
            id="words"
            rows="4"
            class="p-2.5 w-full text-md text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 mt-2 font-sans"
            placeholder="word
word
anotherword..."
            bind:value={textarea}
          />
          <h4 class="font-sans font-light">
            Note: only enter one word per line
          </h4>
          <h3 class="font-sans font-bold text-xl mt-5">Generate:</h3>
          <div class="flew flew-row flex-wrap justify-around">
            <button
              on:click={() => fetch_handler("textFile")}
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 m-2 rounded"
              >Text File (.txt)</button
            >
            <button
              on:click={() => fetch_handler("docxFile")}
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 m-2 rounded"
              >Word File (.docx)</button
            >
            <button
              on:click={() => fetch_handler("pdfFile")}
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 m-2 rounded"
              >PDF File (.pdf)</button
            >
          </div>
        </div>
      </div>
    </div>
  </div>
  {#if loading}
    <button
      on:click={() => (loading = false)}
      class="fixed bottom-4 right-4 z-50 rounded-md bg-green-500 px-6 py-3 text-white transition hover:bg-green-600 translate-x-3"
    >
      <div class="flex items-center space-x-2">
        <span class="text-3xl"><i class="bx bx-check" /></span>
        <p class="font-bold font-sans">You File Is Being Generated...</p>
      </div>
    </button>
  {/if}
</main>

<style global lang="postcss">
  @tailwind utilities;
  @tailwind components;
  @tailwind base;
</style>
