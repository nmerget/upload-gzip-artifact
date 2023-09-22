# Upload Gzip Artifact

This is a simple action to tar a directory/file into a tar.gz file and uploads it as artifact.
This wil increase the speed for large build when using reusable workloads and/or parallel workflows.

## How to use

`````yaml
---
name: Default Pipeline

on:
  pull_request:

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - name: ⏬ Checkout repo
        uses: actions/checkout@v3

      - name: 🔄 Init Cache
        uses: nmerget/npm-cache-action@v1.0.0

      - name: 🔨 Build
        run: npm run build

      - name: ⏫ Upload build
        uses: nmerget/upload-gzip-artifact@v1.0.0
        with:
          name: frontend-build
          path: dist

`````

## Configuration

````yaml
...
- name: ⏫ Upload build
  uses: nmerget/upload-tar-artifact@v1.0.0
  with:
    name: frontend-build # use a good name because this will be shown in GitHub summary, don't use the same name as `path`
    path: dist # your directory to upload
    retention-days: 5 # delete the artifact at some point
...
````

