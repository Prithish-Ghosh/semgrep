VER=v1.0.0     # change per release
MAJOR=v1

# point internal references at this exact version
sed -i -E "s#(Prithish-Ghosh/semgrep/[^ ]*)@v[0-9][0-9.]*#\1@${VER}#g" .github/workflows/*.yml
grep -rn "Prithish-Ghosh/semgrep" .github | grep -v "@${VER}" && echo "CHECK THESE"

git add -A
git commit -m "release ${VER}"
git push origin main

git tag "${VER}"
git tag -f "${MAJOR}"
git push origin "${VER}"
git push -f origin "${MAJOR}"



------------------------------------------------


jobs:
  quality:
    uses: Prithish-Ghosh/semgrep/.github/workflows/quality-gates.yml@v1
    permissions:
      contents: read
      pull-requests: write