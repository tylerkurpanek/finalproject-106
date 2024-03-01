<script>
  import { onMount } from 'svelte';
  import { select } from 'd3-selection';
  import { arc } from 'd3-shape';
  import { scaleLinear } from 'd3-scale';

  let svg;

  const court = () => {
    const usableWidth = 750; // Adjust as needed
    const height =750; // Adjust as needed
    const margins = 10 // Adjust as needed
    const basketRadius = 9; // Adjust as needed
    const pi = Math.PI;
    const threeAngle = 22; // Adjust as needed

    const x = scaleLinear().domain([-10, 10]).range([margins, usableWidth - margins]);
    const y = scaleLinear().domain([0, 25]).range([margins, height - margins]);
    const basket = y(4.75);

    const svg = select('svg')
      .attr('width', usableWidth)
      .attr('height', height);

    const g = svg.append('g')
      .attr('transform', `translate(${margins},${margins})`)
      .style('fill', 'none')
      .style('stroke', '#000');

    // Basket
    g.append('circle')
      .attr('r', basketRadius)
      .attr('cx', x(0))
      .attr('cy', y(4.75));

    // Backboard
    g.append('rect')
      .attr('x', x(-3))
      .attr('y', basket)
      .attr('width', x(3) - x(-3))
      .attr('height', 1);

    // Outer paint
    g.append('rect')
      .attr('x', x(-8))
      .attr('y', y(0))
      .attr('width', x(8) - x(-8))
      .attr('height', y(15) + basket);

    // Inner paint
    g.append('rect')
      .attr('x', x(-6))
      .attr('y', y(0))
      .attr('width', x(6) - x(-6))
      .attr('height', y(15) + basket);

    // Restricted area
    g.append('path')
      .attr('d', arc(x(4) - x(0), 90 * pi, 270 * pi))
      .attr('transform', `translate(${x(0)}, ${basket})`);

    // Free throw
    g.append('path')
      .attr('d', arc(x(6) - x(0), 90 * pi, 270 * pi))
      .attr('transform', `translate(${x(0)}, ${y(15) + basket})`);

    // Free throw dotted
    g.append('path')
      .attr('d', arc(x(6) - x(0), -90 * pi, 90 * pi))
      .attr('stroke-dasharray', '3,3')
      .attr('transform', `translate(${x(0)}, ${y(15) + basket})`);

    // 3-point lines
    g.append('line')
      .attr('x1', x(-22))
      .attr('x2', x(22))
      .attr('y1', y(22))
      .attr('y2', y(22));

    g.append('line')
      .attr('x1', x(-22))
      .attr('x2', x(22))
      .attr('y1', y(25))
      .attr('y2', y(25));

    // 3-point arc
    g.append('path')
      .attr('d', arc(y(23.75), (threeAngle + 90) * pi, (270 - threeAngle) * pi))
      .attr('transform', `translate(${x(0)}, ${basket + basketRadius})`);

    // Half court outer
    g.append('path')
      .attr('d', arc(x(6) - x(0), -90 * pi, 90 * pi))
      .attr('transform', `translate(${x(0)}, ${y(47)})`);

    // Half court inner
    g.append('path')
      .attr('d', arc(x(2) - x(0), -90 * pi, 90 * pi))
      .attr('transform', `translate(${x(0)}, ${y(47)})`);

    // Half court line
    g.append('line')
      .attr('x1', x(-25))
      .attr('x2', x(25))
      .attr('y1', y(47))
      .attr('y2', y(47));

    // Boundaries
    g.append('rect')
      .style('stroke', '#ddd')
      .attr('x', x(-25))
      .attr('y', y(0))
      .attr('width', x(25))
      .attr('height', y(47));

    return svg.node();
  };

  const drawBasketballCourt = () => {
    svg = court();
  };

  onMount(() => {
    drawBasketballCourt();
  });
</script>

<main>
  <h1>Svelte template</h1>

  <!-- SVG container for basketball court -->
  <svg></svg>

  <p>Write your HTML here</p>
</main>

<style>
  /* Write your CSS here */
</style>