#CRDTb

A set of automatically mergeable data structures for dealing with sharded databases that are gossiped together.

- Every shard is like a kafka partition.  Events within a `partition` are totally ordered.

- References to other events must be fully qualified by `partition:eventid`, while even event has an id `partition:eventid` where `eventid` is strictly increasing.

- In addition to the eventid, there must be an increasing `eventts` that denotes when the event was locally created.

To observe every event, get all events in `eventts` order.
To diff between two databases, `all: events[partition][eid : eid > highestknown[partition][eventid]]`, which is a CRDT structure.

If there is a reference to an event, we must catch  up on all events within that partition up to the referenced event.
