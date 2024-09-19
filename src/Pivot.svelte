<script>
    import { onMount, onDestroy } from "svelte";
    import { Pivot } from "@dhx/trial-pivot";
    import "@dhx/trial-pivot/dist/pivot.css";
    
    export let fields;
    export let dataset;

    let container;
    let table;

    onMount(() => {
        table = new Pivot(container, {
            fields,
            data: dataset,
            headerShape: {
                collapsible: true
            },
            tableShape: {
                tree: true,
                templates: ["profit", "sales"].reduce((acc, field) => (acc[field] = v => (v ? Math.ceil(v) : ""), acc), {})
            },
            columnShape: {
                autoWidth: {
                    auto: true,
                    columns: {
                        type: true,
                        title: true
                    },
                    firstOnly: false,
                },
            },
            config: {
                rows: ["state", "product_type"],
                columns: ["product_line", "type"],
                values: [
                    {
                        field: "profit",
                        method: "sum"
                    },
                    {
                        field: "sales",
                        method: "sum"
                    },
                    {
                        field: "date",
                        method: "min"
                    }
                ]
            }
        });
    });
    
    onDestroy(() => {
        table.destructor();
    });
</script>

<div bind:this={container} class="widget"></div>
