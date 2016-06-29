---
layout: docs
title: Migrating from 1.x to 2.x
description: "Guide on migrating from version 1.x (Monifu) to version 2.x"
---

Package renamings:

- `monifu.concurrent` -> `monix.execution`
- `monifu.reactive` -> `monix.reactive`

Moved types:

- `monifu.reactive.Ack` -> `monix.execution.Ack`
- `monifu.reactive.observers.SynchronousObserver` -> `monix.reactive.observers.SyncObserver`
- `monifu.reactive.Subscriber` -> `monix.reactive.observers.Subscriber`
- `monifu.concurrent.extensions` -> `monix.execution.FutureUtils.extensions`
- the `atomic.padded` package in `monifu.concurrent` is now gone, use
  the `Atomic.withPadding` constructor instead

Renamed operators:

- `Observable.lift` -> `Observable.transform`
- `Observable.onSubscribe` -> `Observable.unsafeSubscribeFn` (this one
  changed signature as well, it now returns a `Cancelable` instead of
  `Unit`)
- `Observable.create` -> `Observable.unsafeCreate` and there's a new
  `Observable.create` with different behavior
- `Ack.Cancel` -> `Ack.Stop`
- for the `FutureUtils` extensions `withTimeout` was renamed to
  `timeout` and `liftTry` to `materialize`, for consistency with
  `Task`
- `Observable.from` is `Observable.apply` and `Observable.unit` was
  renamed to `Observable.now`
- `Observable.whileBusyDropEvents(onOverflow)` renamed to
  `Observable.whileBusyDropEventsAndSignal`
- `Observable.toReactive` -> `toReactivePublisher`
- `Cancelable.apply` now wants a `Function0` and not a by-name parameter

The `Channel` type is now gone, replaced by:

- `monix.reactive.observers.SyncObserver` for describing just
  synchronous input
- `monix.reactive.subjects.ConcurrentSubject` for describing
  synchronous input with attached output

`Future` no longer converts to `Observable` automatically. Use
`Observable.fromFuture`.