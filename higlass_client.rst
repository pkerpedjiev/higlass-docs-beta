HiGlass Client (Developer)
##########################

View configs (viewconfs)
========================

The entire state of a HiGlass composition is defined in a **viewconfig** file.
This is a JSON declaration of what data should be displayed, where it should be
displayed and how it should be rendered.

All uids are optional. If they aren't specified, they will be randomly generated.
Note that if there are any locks, the uuids

Overlays
--------

Overlays highlight regions in other tracks. The tracks it highlights are specified
in the `includes` field. The extent is the region that will be highlighted in that
field. If the track is a 1D track, only the first part of the extent will be used.
The extent uses absolute coordinates so any translation between genomic and
absolute coordinates needs to be performed elsewhere.

.. code-block:: json

    {
        "overlays": [
            {
                uid: 'aa',
                includes: ['track1Uid', 'track2Uid'],
                options: [
                    extent: [[0,10000],[3000,4000]]
                ]
            }
        ]
    }
    


1D Tracks
*********

Line Tracks
===========

Scaling
-------


1D tracks can either be linearly or log scaled. Linear scaling denotes a linear
mapping between the values and their position on the track. Log scaling means
that we take the log of the values before positioning them. 

Because the dataset may contain very small or even zero values, we add a
pseudocount equal to the median visible value to ensure that finer details in
the data are not drowned out by extreme small values.

The code for this can be found in ``HorizontalLine1DPixiTrack.drawTile``.


Interface
---------

visibleAndFetchedIds: Tile ids that correspond to tiles which are both visible
in the current viewport as well as fetched from the server.

visibleTileIds: Tiles which should be visible in the current viewport based on
the current viewport. Usually set by ``calculateVisibleTiles``.
