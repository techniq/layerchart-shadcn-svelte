<script>
  import { Button } from "$lib/components/ui/button";
  import {
    Area,
    Axis,
    Chart,
    Highlight,
    Svg,
    Tooltip,
    TooltipItem,
  } from "layerchart";
  import { scaleTime } from "d3-scale";

  import appleStock from "./apple-stock.json";

  const data = appleStock.map((d) => {
    return { date: new Date(d.date), value: d.value };
  });
</script>

<div class="h-[300px] p-4 border rounded">
  <Chart
    {data}
    x="date"
    xScale={scaleTime()}
    y="value"
    yDomain={[0, null]}
    yNice
    padding={{ left: 16, bottom: 24 }}
    tooltip={{ mode: "bisect-x" }}
  >
    <Svg>
      <Axis placement="left" grid rule />
      <Axis placement="bottom" rule />
      <Area
        line={{ class: "stroke-2 stroke-primary" }}
        class="fill-primary/30"
      />
      <Highlight points lines />
    </Svg>

    <!-- header={(data) => formatDate(data.date, "eee, MMMM do")} -->
    <Tooltip _variant="invert" let:data>
      <TooltipItem label="value" value={data.value} />
    </Tooltip>
  </Chart>
</div>

<Button>Click me</Button>
