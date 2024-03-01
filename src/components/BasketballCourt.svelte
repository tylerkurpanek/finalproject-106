court = {
    const svg = d3.select(DOM.svg(usableWidth, height))
    
    const g = svg.append('g')
      .attr('transform', `translate(${[margins,margins]})`)
      .style('fill', 'none')
      .style('stroke', '#000')
    
    // basket
    g.append('circle')
      .attr('r', basketRadius)
      .attr('cx', x(0))
      .attr('cy', y(4.75))
    
    // backboard
    g.append('rect')
      .attr('x', x(-3))
      .attr('y', basket)
      .attr('width', x(3) - x(-3))
      .attr('height', 1)
    
    // outer paint
    g.append('rect')
      .attr('x', x(-8))
      .attr('y', y(0))
      .attr('width', x(8) - x(-8))
      .attr('height', y(15) + basket)
    
    // inner paint
    g.append('rect')
      .attr('x', x(-6))
      .attr('y', y(0))
      .attr('width', x(6) - x(-6))
      .attr('height', y(15) + basket)
  
    // restricted area
    g.append('path')
      .attr('d', arc(x(4) - x(0), 90 * pi, 270 * pi))
      .attr('transform', `translate(${[x(0), basket]})`)
  
    // freethrow
    g.append('path')
      .attr('d', arc(x(6) - x(0), 90 * pi, 270 * pi))
      .attr('transform', `translate(${[x(0), y(15) + basket]})`)
    
    // freethrow dotted
    g.append('path')
      .attr('d', arc(x(6) - x(0), -90 * pi, 90 * pi))
      .attr('stroke-dasharray', '3,3')
      .attr('transform', `translate(${[x(0), y(15) + basket]})`)
    
    // 3-point lines
    g.append('line')
      .attr('x1', x(-21.775)) // lines up the stroke a little better than the true 22 ft.
      .attr('x2', x(-21.775))
      .attr('y2', y(14))
    
    g.append('line')
      .attr('x1', x(21.775))
      .attr('x2', x(21.775))
      .attr('y2', y(14))
    
    // 3-point arc
    g.append('path')
      .attr('d', arc(y(23.75), (threeAngle + 90) * pi, (270 - threeAngle) * pi))
      .attr('transform', `translate(${[x(0), basket + basketRadius]})`)
  
    // half court outer
    g.append('path')
      .attr('d', arc(x(6) - x(0), -90 * pi, 90 * pi))
      .attr('transform', `translate(${[x(0), y(47)]})`)
    
    // half court inner
    g.append('path')
      .attr('d', arc(x(2) - x(0), -90 * pi, 90 * pi))
      .attr('transform', `translate(${[x(0), y(47)]})`)
    
    // half court line
    g.append('line')
      .attr('x1', x(-25))
      .attr('x2', x(25))
      .attr('y1', y(47))
      .attr('y2', y(47))
    
    // boundaries
    g.append('rect')
      .style('stroke', '#ddd')
      .attr('x', x(-25))
      .attr('y', y(0))
      .attr('width', x(25))
      .attr('height', y(47))
          
    
    return svg.node();
  }