Running `tsgo --listFilesOnly` produces inconsistent results in this repo. `tsc` does not have this behavior.

What negative effects come from that are unclear, perhaps breaking build caching, or leading to strange random failures.

To get this minimal repro I've had to import directly from `node_modules` in an unusual way. It's possible this problem can only be caused that way, or maybe it can happen with other kinds of absolute or aliased imports.

```bash
pnpm install
# No diff
diff <(pnpm exec tsc --listFilesOnly | sort) <(pnpm exec tsc --listFilesOnly | sort)
# Large diff (almost always)
diff <(pnpm exec tsgo --listFilesOnly | sort) <(pnpm exec tsgo --listFilesOnly | sort)
```

`index.ts`:
```ts
import { type DataGridProProps } from '@mui/x-data-grid-pro';
import { type GridRowParams } from './node_modules/@mui/x-data-grid/models/params';
```
