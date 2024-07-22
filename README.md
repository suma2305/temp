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
      const states = topojson.feature(us, us.objects.states).features;

      svg.append('g')
        .selectAll('path')
        .data(states)
        .enter().append('path')
        .attr('d', path)
        .attr('fill', '#ccc')
        .attr('stroke', '#333');

      svg.selectAll('g')
        .data(states)
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
}
```


```
import { Component, OnInit, OnChanges } from '@angular/core';
import * as Highcharts from "highcharts/highmaps";
import Drilldown from 'highcharts/modules/drilldown';
Drilldown(Highcharts);

declare var require: any;
const usaMap = require("@highcharts/map-collection/countries/us/us-all.geo.json");

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent implements OnInit  {
  Highcharts;
    chartConstructor = "mapChart";
    chartOptions;

    constructor() { }

    ngOnInit() {
        this.Highcharts = Highcharts;

        this.chartOptions = {
            chart: {
                map: usaMap,
            },
            series: [
                {
                    data: [{
                        id: "us-co",
                        drilldown: "us-co",
                        value: 100
                    }],
                    mapData: usaMap,
                    allowPointSelect: true,
                    joinBy: ["hc-key", "id"]
                }
            ],
            drilldown: {
                series: [
                    {
                        name: "us-co",
                        id: "us-co",
                        data: [
                           ['us-co-080', 34],
                            ['us-co-081', 33],
                            ['us-co-082', 33]
                        ]
                    }
                ]
            }
        };
    }

    

}


```

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
      console.log('US Data:', us);  // Debugging line
      const states = topojson.feature(us, us.objects.states).features;

      console.log('States Features:', states);  // Debugging line

      svg.append('g')
        .selectAll('path')
        .data(states)
        .enter().append('path')
        .attr('d', path)
        .attr('fill', '#ccc')
        .attr('stroke', '#333');

      svg.selectAll('g')
        .data(states)
        .enter().append('g')
        .attr('class', 'state-button-group')
        .each((d: any, i, nodes) => {
          const stateId = d.id;
          const stateName = d.properties.name;

          if (this.data[stateId]) {
            const [x, y] = path.centroid(d);

            d3.select(nodes[i])
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
    }).catch(error => {
      console.error('Error loading or parsing data:', error);
    });
  }
}

```
```
[8:52 PM, 7/21/2024] Tinku USA: import { Component, AfterViewInit } from '@angular/core';
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

    const path = d3.geoPath().pro…
[9:26 PM, 7/21/2024] Tinku USA: import { Component, AfterViewInit } from '@angular/core';
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
      // Log the data to understand its structure
      console.log('US Data:', us);

      // Extract the features from TopoJSON
      const states = topojson.feature(us, us.objects.states).features;

      // Log the features to understand their structure
      console.log('States Features:', states);

      svg.append('g')
        .selectAll('path')
        .data(states)
        .enter().append('path')
        .attr('d', path)
        .attr('fill', '#ccc')
        .attr('stroke', '#333');

      svg.selectAll('g')
        .data(states)
        .enter().append('g')
        .attr('class', 'state-button-group')
        .each((d: any, i, nodes) => {
          const stateId = d.id;
          const stateName = d.properties.name;

          if (this.data[stateId]) {
            const [x, y] = path.centroid(d);

            const g = d3.select(nodes[i]); // Access the current node

            g.append('foreignObject')
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
    }).catch(error => {
      console.error('Error loading or parsing data:', error);
    });
  }
}
```
```
https://github.com/jcbowyer/d3-in-angular/blob/master/src/app/unitedstates-map/unitedstates-map.component.ts
```
