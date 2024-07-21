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


```// us-map.component.ts
import { Component, OnInit } from '@angular/core';
import * as d3 from 'd3';
import * as topojson from 'topojson-client';

@Component({
  selector: 'app-us-map',
  templateUrl: './us-map.component.html',
  styleUrls: ['./us-map.component.css']
})
export class UsMapComponent implements OnInit {
  private data = { "AZ": 1, "TX": 2 };

  constructor() { }

  ngOnInit(): void {
    this.createMap();
  }

  private createMap(): void {
    const width = 960;
    const height = 600;

    const svg = d3.select('svg')
      .attr('width', width)
      .attr('height', height);

    const projection = d3.geoAlbersUsa()
      .scale(1000)
      .translate([width / 2, height / 2]);

    const path = d3.geoPath()
      .projection(projection);

    d3.json('assets/us.topo.json').then((us: any) => {
      const states = topojson.feature(us, us.objects.states);

      svg.append('g')
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
        .text((d: any) => this.data[d.properties.name] ? 'Button' : '');
    });
  }
}```

```createMap(): void {
    const width = 960;
    const height = 600;

    const svg = d3.select('#us-map-container').append('svg')
      .attr('width', width)
      .attr('height', height);

    const projection = d3.geoAlbersUsa()
      .scale(1280)
      .translate([width / 2, height / 2]);

    const path = d3.geoPath()
      .projection(projection);

    const g = svg.append('g');

    // Draw the map
    g.selectAll('path')
      .data(topojson.feature(usMapData, usMapData.objects.states).features)
      .enter().append('path')
      .attr('d', path)
      .attr('class', 'state');

    // Add buttons to the states with counts
    g.selectAll('circle')
      .data(topojson.feature(usMapData, usMapData.objects.states).features)
      .enter().append('circle')
      .attr('cx', d => path.centroid(d)[0])
      .attr('cy', d => path.centroid(d)[1])
      .attr('r', d => this.stateCounts[d.id] ? 10 : 0) // Adjust radius based on count
      .attr('class', 'state-button')
      .style('fill', 'red')
      .on('click', d => alert(State: ${d.properties.name}, Count: ${this.stateCounts[d.id]}));
  }
createMap(): void {
    const width = 960;
    const height = 600;

    const svg = d3.select('#us-map-container').append('svg')
      .attr('width', width)
      .attr('height', height);

    const projection = d3.geoAlbersUsa()
      .scale(1280)
      .translate([width / 2, height / 2]);

    const path = d3.geoPath()
      .projection(projection);

    const g = svg.append('g');

    // Draw the map
    g.selectAll('path')
      .data(topojson.feature(usMapData, usMapData.objects.states).features)
      .enter().append('path')
      .attr('d', path)
      .attr('class', 'state');

    // Add buttons to the states with counts
    g.selectAll('circle')
      .data(topojson.feature(usMapData, usMapData.objects.states).features)
      .enter().append('circle')
      .attr('cx', d => path.centroid(d)[0])
      .attr('cy', d => path.centroid(d)[1])
      .attr('r', d => this.stateCounts[d.id] ? 10 : 0) // Adjust radius based on count
      .attr('class', 'state-button')
      .style('fill', 'red')
      .on('click', d => alert(State: ${d.properties.name}, Count: ${this.stateCounts[d.id]}));
  }```
