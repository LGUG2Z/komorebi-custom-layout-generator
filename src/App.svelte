<script>

    export let tertiary_column_windows = 4;
    export let columns = [
        {
            "column": "Primary"
        },
        {
            "column": "Tertiary",
            "configuration": "Horizontal"
        }
    ]

    function add_column() {
        columns.unshift({"column": "Secondary"})
        columns = columns
    }

    function remove_column(i) {
        columns.splice(i, 1)
        columns = columns
    }

    function add_row(i) {
        if (columns[i].configuration == null) {
            columns[i].configuration = {
                "Horizontal": 2
            }
        } else {
            columns[i].configuration.Horizontal += 1;
        }

        columns = columns
    }

    function remove_row(i) {
        if (columns[i].configuration.Horizontal === 2) {
            columns[i] = {
                "column": "Secondary"
            }

            return
        }

        if (columns[i].configuration.Horizontal !== 1) {
            columns[i].configuration.Horizontal -= 1;
        }

        columns = columns
    }

    function move_left(i) {
        if (i !== 0) {
            let current = columns[i];
            columns[i] = columns[i - 1];
            columns[i - 1] = current;
        }

        columns = columns
    }

    function move_right(i) {
        if (i !== columns.length - 2) {
            let current = columns[i];
            columns[i] = columns[i + 1];
            columns[i + 1] = current;
        }

        columns = columns
    }
</script>

<main class="text-center">
    <div class="h-screen p-10 grid grid-cols-4 gap-5">
        <div class="col-span-3 rounded-none border-2 p-5 border-black">
            <div class="h-full grid grid-cols-{columns.length} grid-rows-1 gap-5">
                {#each columns as column, i}
                    {#if column.column === "Primary"}
                        <div class="flex bg-blue-200 min-h-full items-center justify-center">
                            <div>
                                <p class="font-semibold text-2xl">Primary</p>
                                {#if i === 0}
                                    <br/>
                                    <button type="button"
                                            on:click={() => add_column()}
                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                        + Col
                                    </button>
                                {/if}
                                <br/>
                                {#if i !== 0}
                                    <button type="button"
                                            on:click={() => move_left(i)}
                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                        ←
                                    </button>
                                {/if}
                                {#if i !== columns.length - 2}
                                    <button type="button"
                                            on:click={() => move_right(i)}
                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                        →
                                    </button>
                                {/if}
                            </div>
                        </div>
                    {/if}

                    {#if column.column === "Secondary"}
                        {#if column.configuration == null}
                            <div class="flex bg-gray-200 min-h-full items-center justify-center">
                                <div>
                                    <p class="font-semibold text-2xl">Secondary</p>
                                    <br/>
                                    {#if i === 0}
                                        <button type="button"
                                                on:click={() => add_column()}
                                                class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                            + Col
                                        </button>
                                    {/if}
                                    <button type="button"
                                            on:click={() => remove_column(i)}
                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                        - Col
                                    </button>
                                    <br/>
                                    <button type="button"
                                            on:click={() => add_row(i)}
                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                        + Row
                                    </button>
                                    <br/>
                                    {#if i !== 0}
                                        <button type="button"
                                                on:click={() => move_left(i)}
                                                class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                            ←
                                        </button>
                                    {/if}
                                    {#if i !== columns.length - 2}
                                        <button type="button"
                                                on:click={() => move_right(i)}
                                                class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                            →
                                        </button>
                                    {/if}
                                </div>
                            </div>
                        {:else}
                            <div class="min-h-full grid grid-cols-1 grid-rows-{column.configuration.Horizontal} gap-5">
                                {#each Array(column.configuration.Horizontal) as _, j}
                                    <div class="flex bg-gray-200 min-h-full items-center justify-center">
                                        <div>
                                            <p class="font-semibold text-2xl">Secondary</p>
                                            {#if i === 0 && j === 0}
                                                <br/>
                                                <button type="button"
                                                        on:click={() => add_column()}
                                                        class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                                    + Col
                                                </button>
                                            {/if}
                                            {#if j === 0}
                                                <button type="button"
                                                        on:click={() => remove_column(i)}
                                                        class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                                    - Col
                                                </button>
                                                <br/>
                                                <button type="button"
                                                        on:click={() => add_row(i)}
                                                        class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                                    + Row
                                                </button>
                                                <button type="button"
                                                        on:click={() => remove_row(i)}
                                                        class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                                    - Row
                                                </button>
                                                <br/>
                                                {#if i !== 0}
                                                    <button type="button"
                                                            on:click={() => move_left(i)}
                                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                                        ←
                                                    </button>
                                                {/if}
                                                {#if i !== columns.length - 2}
                                                    <button type="button"
                                                            on:click={() => move_right(i)}
                                                            class="inline-flex items-center px-6 py-3 border border-gray-300 shadow-sm text-base font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                                        →
                                                    </button>
                                                {/if}
                                            {/if}
                                        </div>
                                    </div>
                                {/each}
                            </div>

                        {/if}
                    {/if}

                    {#if column.column === "Tertiary"}
                        <div class="min-h-full grid grid-cols-1 grid-rows-{tertiary_column_windows} gap-5">
                            {#each Array(tertiary_column_windows) as _, _}
                                <div class="flex bg-green-200 min-h-full items-center justify-center">
                                    <div>
                                        <p class="font-semibold text-2xl">Tertiary</p>
                                    </div>
                                </div>
                            {/each}
                        </div>
                    {/if}
                {/each}
            </div>

        </div>
        <div class="flex justify-center items-center bg-gray-800 text-white">
            <div class="text-left">
                <pre><code>{JSON.stringify(columns, null, 2)}</code></pre>
            </div>
        </div>
    </div>
</main>
