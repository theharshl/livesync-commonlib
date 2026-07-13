# Changelog

All notable changes made in this fork (relative to
[vrtmrz/livesync-commonlib](https://github.com/vrtmrz/livesync-commonlib))
are documented here. Upstream history before the fork is not repeated — see
the upstream repo for that.

## [Unreleased] - 2026-07-13

- Fix unhandled crash when no active replicator is available. Widen
  `getActiveReplicator`'s type to `LiveSyncAbstractReplicator | undefined`
  and have `DirectFileManipulator.$getReplicator()` return `undefined`
  instead of throwing — its one real caller
  (`ChunkFetcher.requestMissingChunks`) already null-checks for this. Also
  move the `getByMeta()` call inside `beginWatch()`'s per-document
  try/catch so a single corrupted/unrecoverable document (e.g. a
  `"Load failed"` error) can't escape as an unhandled rejection and crash
  the whole process. (f0b4981, branch `fix/direct-file-manipulator-replicator-stub`)
