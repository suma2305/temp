
```
import { Component, AfterViewInit } from '@angular/core';
import * as d3 from 'd3';
import * as topojson from 'topojson-client';

@Component({
  selector: 'app-us-map',
  templateUrl: './us-map.component.html',
  styleUrls: ['./us-map.component.css']
})
export class UsMapComponent implements AfterViewInit {
  private width = 960;
  private height = 600;
  private data = { "AZ": 1, "TX": 2 };

  constructor() { }

  ngAfterViewInit() {
    this.createMap();
  }

  private createMap(): void {
    const svg = d3.select('#map')
      .append('svg')
      .attr('width', this.width)
      .attr('height', this.height);

    const projection = d3.geoAlbersUsa()
      .scale(1000)
      .translate([this.width / 2, this.height / 2]);

    const path = d3.geoPath().projection(projection);

    d3.json('https://d3js.org/us-10m.v1.json').then((us: any) => {
      svg.append('g')
        .selectAll('path')
        .data(topojson.feature(us, us.objects.states).features)
        .enter().append('path')
        .attr('d', path)
        .attr('fill', '#ccc')
        .attr('stroke', '#333');

      svg.selectAll('g')
        .data(topojson.feature(us, us.objects.states).features)
        .enter().append('g')
        .attr('class', 'state-button-group')
        .each((d: any) => {
          const stateId = d.id;
          const stateName = d.properties.name;
          if (this.data[stateId]) {
            const [x, y] = path.centroid(d);
            d3.select(d3.event.currentTarget)
              .append('foreignObject')
              .attr('x', x - 30)
              .attr('y', y - 15)
              .attr('width', 60)
              .attr('height', 30)
              .append('xhtml:button')
              .attr('class', 'state-button')
              .text('Button')
              .on('click', () => alert(State: ${stateName}, Count: ${this.data[stateId]}));
          }
        });
    });
  }
}```
