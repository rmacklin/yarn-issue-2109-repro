Reproduction repository for https://github.com/yarnpkg/yarn/issues/2109

Steps to reproduce:

1. `git clone git@github.com:rmacklin/yarn-issue-2109-repro.git`
2. `cd yarn-issue-2109-repro`
3. `node yarn-0.17.10.js upgrade left-pad`
4. Observe:

This added a new, untracked tarball for the new version of `left-pad` in the
cache:

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   package.json
	modified:   yarn.lock

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	npm-packages-offline-cache/left-pad-1.1.3.tgz

no changes added to commit (use "git add" and/or "git commit -a")
```

However, the old `npm-packages-offline-cache/left-pad-1.1.2.tgz` tarball was
_not_ removed even though it's no longer used. This means that it has to be
manually deleted (an easy step to forget) in order to prevent the offline cache
from growing to contain many unused packages over time.
