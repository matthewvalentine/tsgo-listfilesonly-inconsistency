Running `tsgo --listFilesOnly` produces inconsistent results in this repo. What negative effects come from that are unclear, perhaps breaking build caching, or leading to strange random failures.

```bash
pnpm install
# No diff
diff <(pnpm exec tsc --listFilesOnly | sort) <(pnpm exec tsc --listFilesOnly | sort)
# Large diff (almost always)
diff <(pnpm exec tsgo --listFilesOnly | sort) <(pnpm exec tsgo --listFilesOnly | sort)
```