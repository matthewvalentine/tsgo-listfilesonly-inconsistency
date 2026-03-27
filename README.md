Running `tsgo --listFilesOnly` produces inconsistent results in this repo. What negative effects come from that are unclear, perhaps breaking build caching, or leading to strange random failures.

To get this minimal repro I've had to import directly from `node_modules` in an unusual way. This problem also exists in a large private repo without an import like that, but I haven't been able to figure out how to make that work here.

```bash
pnpm install
# No diff
diff <(pnpm exec tsc --listFilesOnly | sort) <(pnpm exec tsc --listFilesOnly | sort)
# Large diff (almost always)
diff <(pnpm exec tsgo --listFilesOnly | sort) <(pnpm exec tsgo --listFilesOnly | sort)
```
