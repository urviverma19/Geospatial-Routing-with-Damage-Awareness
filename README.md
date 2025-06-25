🛰️ Geospatial Routing with Damage Awareness
This Python module leverages computer vision, geospatial data, and road network analysis to detect damaged buildings from a segmentation mask and dynamically update the road network cost for routing algorithms.

📌 Features
Geo-context Extraction: Parses geographic metadata from label JSON files and fetches road network data using OSMnx.

Pixel-to-Geo Conversion: Converts pixel-based mask coordinates to projected geographic coordinates.

Damage Detection: Identifies destroyed buildings from mask predictions using OpenCV contours.

Graph Penalization: Increases traversal cost of road segments near destroyed buildings for smarter routing decisions.

🔧 Functions Overview
get_geo_context(json_path)
Parses the geographic bounds from label JSON and fetches the corresponding road network (graph) from OpenStreetMap.

pixel_to_geo(px, py, img_shape, geo_bounds)
Converts pixel coordinates (from the mask) to geographic coordinates (lat/lon), and projects them into the same CRS as the graph.

get_polygons_from_mask(mask, damage_class_id)
Extracts polygons from the predicted mask for a specific class (e.g., class 4 for destroyed buildings).

update_graph_with_damage(G_proj, pred_mask, geo_bounds)
Penalizes roads that are close to destroyed buildings by assigning a high traversal cost, effectively routing traffic away from unsafe areas.

⚙️ Dependencies
osmnx

networkx

shapely

opencv-python

numpy

Install using:

bash
Copy
Edit
pip install osmnx networkx shapely opencv-python numpy
📁 Input/Output
Input:

JSON label file with geographic bounds.

Mask image (NumPy array) with damage classes.

Output:

Updated networkx graph with modified edge costs.

📌 Constants
DESTROYED_BUILDING_COST: Cost assigned to roads near damaged buildings (default: 100000).

ROAD_BUFFER_DISTANCE_METERS: Buffer radius to consider a road affected (default: 15m).
