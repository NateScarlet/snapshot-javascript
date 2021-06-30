# snapshot test for javascript

[![Node CI](https://github.com/NateScarlet/snapshot-javascript/actions/workflows/nodejs.yml/badge.svg)](https://github.com/NateScarlet/snapshot-javascript/actions/workflows/nodejs.yml)
[![npm package](https://img.shields.io/npm/v/@nates/snapshot)](https://www.npmjs.com/package/@nates/snapshot)

## Install

```shell
npm install @nates/snapshot
```

## Usage

A simple setup is required for auto snapshot key, see [mocha example](./tests/setup.ts)

set SNAPSHOT_UPDATE env var to true to update existed snapshot file.

```typescript
import snapshot from '@nates/snapshot';

const value = { a: 1 };

// basic
await snapshot.match(value); // throw error if value not match previous run

// store snapshot file as json
await snapshot.matchJSON(value);

// use different snapshot file
await snapshot.matchJSON(value, { key: snapshot.getKey('second') });

// clean dynamic data
await snapshot.match(new Date(), {
  clean: (v) => v.replace(/(?<="\$Date": ").+(?=")/g, snapshot.maskString),
});
```

## Implementation for other language

- [Go](https://github.com/NateScarlet/snapshot)
