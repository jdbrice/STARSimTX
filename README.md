## STARSim Stand Alone Workflow 
===

This workflow is primarily a tutorial for how to run STARsim in stand alone mode with TX files as input.

1. Run your Event Generator (EG) to produce the TX files (eg. STARlight, UrQMD, etc.)
2. Run STARsim via "kumac" script. See StarSim.kumac for a working example. This file should work without modification if the proper command-line options are passed in.
 - See the STARSIM.xml for an example star-submit file for running on RCF cluster
3. Verify that step 2 produced .fz files - GEANT "zebra" files. 
4. Run the BFC to convert the .fz files to STAR ROOT formats (StMCEvent etc.) and optionally do event reconstruction.
 - Example coming soon

Overview of TX file format:
See : [TX_Format](http://www.star.bnl.gov/public/comp/simu/gstar/Manual/txformat.html)

EVENT: {event_index} {n_tracks} {n_vertices} 
- event_index = unique event index (starts at 1)
- n_tracks = number of tracks in event
- n_vertices = number of vertices in event

VERTEX: {vX} {vY} {vZ} {time} {vertex_index} {process} {parent_track} {n_daughters}  
- vX, vY, vZ = vertex position (x,y,z) in [cm]
- time = Time of collision/vertex formation (0 for primary vertex)
- vertex_index = unique vertex index (starts at 1)
- process = physical process (arbitrary label, passed-through)
- parent_track = parent track of this vertex (for decays), 0 for primary vertex 
- n_daughters = Number of daughter tracks originating from this vertex

TRACK: {GEANT_pid} {pX} {pY} {pZ} {track_index} {start_vertex} {stop_vertex} {eg_pid}
- GEANT_pid = GEANT’s particle id code
- pX, pY, pZ = Track momentum in GeV/c
- track_index = unique track index (starts at 1) (passed-through)
- start_vertex/stop_veretx = the ids of the vertex at which the track starts and stops
- eg_pid = Event Generator’s PID code (not used, passed-through)