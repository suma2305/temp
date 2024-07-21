# temp

 ```svg.append('g')
        .selectAll('path')
        .data(states.features)
        .enter().append('path')
        .attr('d', path)
        .attr('class', 'state')
        .style('fill', (d: any) => {
          return this.data[d.properties.name] ? 'blue' : 'gray';
        });

      svg.append('g')
        .selectAll('text')
        .data(states.features)
        .enter().append('text')
        .attr('x', (d: any) => projection(d3.geoCentroid(d))[0])
        .attr('y', (d: any) => projection(d3.geoCentroid(d))[1])
        .attr('dy', '.35em')
        .style('text-anchor', 'middle')
        .text((d: any) => this.data[d.properties.name] ? 'Button' : '');```



        https://github.com/jgoodall/us-maps/blob/master/topojson/state.topo.json?short_path=af597f1
