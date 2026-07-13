The common library of Self-hosted LiveSync and its series.

License: MIT

## About this fork

This is [theharshl](https://github.com/theharshl)'s fork of
[vrtmrz/livesync-commonlib](https://github.com/vrtmrz/livesync-commonlib),
used as the `lib` git submodule of
[theharshl/obsidian-livesync-bridge](https://github.com/theharshl/obsidian-livesync-bridge).

`DirectFileManipulator` (the lightweight direct-CouchDB-API client used by
that bridge) has no live P2P/replication layer, but upstream's
`$getReplicator()` threw `"Method not implemented."` instead of returning
`undefined` as its one real caller already expected — crashing the whole
bridge process via an unhandled promise rejection whenever a missing chunk
had to be fetched. This fork fixes that (and a related unguarded
`getByMeta()` call in `beginWatch()`) without otherwise diverging from
upstream. See [CHANGELOG.md](./CHANGELOG.md) for the exact commits.