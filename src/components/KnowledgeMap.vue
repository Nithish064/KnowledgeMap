<template>
  <div class="knowledge-map-container">
    <h1>Map of Knowledge</h1>
    <div id="knowledge-map"></div>
  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  name: "KnowledgeMap",
  data() {
    return {
      nodes: [
        { id: "0. Foundations", group: 1 },
        { id: "1. Basic ROS2", group: 2 },
        { id: "2. ROS Basics", group: 2 },
        { id: "3. Intermediate ROS2", group: 3 },
        { id: "4. Robotics Theory", group: 3 },
        { id: "5. Navigation ROS2", group: 4 },
        { id: "6. Behavior Trees for ROS2", group: 4 },
        { id: "7. Manipulation", group: 5 },
        { id: "8. Robot Creation", group: 5 },
        { id: "9. Artificial Intelligence", group: 6 },
        { id: "10. ROS Debugging", group: 6 },
        { id: "11. Course of product", group: 6 },
        { id: "12. Web Development for Robots", group: 7 },
        { id: "13. Simulation", group: 7 },
        { id: "14. Enterprise", group: 8 },
      ],
      links: [
        { source: "0. Foundations", target: "1. Basic ROS2" },
        { source: "1. Basic ROS2", target: "2. ROS Basics" },
        { source: "1. Basic ROS2", target: "3. Intermediate ROS2" },
        { source: "3. Intermediate ROS2", target: "4. Robotics Theory" },
        { source: "3. Intermediate ROS2", target: "5. Navigation ROS2" },
        { source: "5. Navigation ROS2", target: "6. Behavior Trees for ROS2" },
        { source: "5. Navigation ROS2", target: "7. Manipulation" },
        { source: "7. Manipulation", target: "8. Robot Creation" },
        { source: "3. Intermediate ROS2", target: "9. Artificial Intelligence" },
        { source: "9. Artificial Intelligence", target: "10. ROS Debugging" },
        { source: "10. ROS Debugging", target: "12. Web Development for Robots" },
        { source: "3. Intermediate ROS2", target: "11. Course of product" },
        { source: "0. Foundations", target: "13. Simulation" },
        { source: "13. Simulation", target: "14. Enterprise" },
      ],
    };
  },
  mounted() {
    this.drawKnowledgeMap();
  },
  methods: {
    drawKnowledgeMap() {
      const width = 1000;
      const height = 800;

      // Create SVG container
      const svg = d3
        .select("#knowledge-map")
        .append("svg")
        .attr("width", width)
        .attr("height", height)
        .style("border", "1px solid lightgray");

      // Define simulation (force-directed graph)
      const simulation = d3
        .forceSimulation(this.nodes)
        .force("link", d3.forceLink(this.links).id((d) => d.id).distance(150))
        .force("charge", d3.forceManyBody().strength(-400))
        .force("center", d3.forceCenter(width / 2, height / 2));

      // Define links (edges)
      const link = svg
        .selectAll("line")
        .data(this.links)
        .enter()
        .append("line")
        .attr("stroke", "#999")
        .attr("stroke-width", 2);

      // Define nodes (circles)
      const node = svg
        .selectAll("circle")
        .data(this.nodes)
        .enter()
        .append("circle")
        .attr("r", (d) => (d.group === 1 ? 10 : 7)) // Main nodes are larger
        .attr("fill", (d) => this.getNodeColor(d.group))
        .call(
          d3
            .drag()
            .on("start", this.dragStarted(simulation))
            .on("drag", this.dragged)
            .on("end", this.dragEnded(simulation))
        );

      // Add labels to nodes
      const label = svg
        .selectAll("text")
        .data(this.nodes)
        .enter()
        .append("text")
        .attr("dx", 12)
        .attr("dy", 4)
        .style("font-size", "10px")
        .style("font-family", "Arial")
        .text((d) => d.id);

      // Update positions on each simulation tick
      simulation.on("tick", () => {
        link
          .attr("x1", (d) => d.source.x)
          .attr("y1", (d) => d.source.y)
          .attr("x2", (d) => d.target.x)
          .attr("y2", (d) => d.target.y);

        node.attr("cx", (d) => d.x).attr("cy", (d) => d.y);

        label.attr("x", (d) => d.x).attr("y", (d) => d.y);
      });
    },
    // Function to color nodes based on group
    getNodeColor(group) {
      const colors = [
        "#FF5733", // Group 1 (orange)
        "#3498DB", // Group 2 (blue)
        "#2ECC71", // Group 3 (green)
        "#9B59B6", // Group 4 (purple)
        "#F1C40F", // Group 5 (yellow)
        "#E74C3C", // Group 6 (red)
        "#34495E", // Group 7 (gray)
        "#1ABC9C", // Group 8 (cyan)
      ];
      return colors[group % colors.length];
    },
    // Dragging functions
    dragStarted(simulation) {
      return function (event, d) {
        if (!event.active) simulation.alphaTarget(0.3).restart();
        d.fx = d.x;
        d.fy = d.y;
      };
    },
    dragged(event, d) {
      d.fx = event.x;
      d.fy = event.y;
    },
    dragEnded(simulation) {
      return function (event, d) {
        if (!event.active) simulation.alphaTarget(0);
        d.fx = null;
        d.fy = null;
      };
    },
  },
};
</script>

<style scoped>
.knowledge-map-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #f9f9f9;
  padding: 20px;
}

#knowledge-map {
  margin-top: 10px;
}
</style>
