## `vendir.yml` spec

```yaml
apiVersion: vendir.k14s.io/v1alpha1
kind: Config

# declaration of minimum required vendir binary version (optional)
minimumRequiredVersion: 0.8.0

# one or more directories to manage with vendir
directories:
- # path is relative to vendir.yml location
  path: config/_ytt_lib

  contents:
  - # path lives relative to directory path # (required)
    path: github.com/cloudfoundry/cf-k8s-networking

    # uses git to clone repository (optional)
    git:
      # http or ssh urls are supported (required)
      url: https://github.com/cloudfoundry/cf-k8s-networking
      # branch, tag, commit; origin is the name of the remote (required)
      ref: origin/master

    # fetches assets from a github release
    githubRelease:
      # slug for repository (org/repo) (required)
      slug: k14s/kapp-controller
      # use release tag (optional)
      tag: v0.1.0
      # use latest published version (optional)
      latest: true
      # use exact release URL (optional)
      url: https://api.github.com/repos/k14s/kapp-controller/releases/21912613
      # checksums for downloaded files (optional)
      # (if release text body contains checksums, it's not necessary
      # to manually specify them here)
      checkums:
        release.yml: 26bf09c42d72ae448af3d1ee9f6a933c87c4ec81d04d37b30e1b6a339f5983a7
      # disables checking auto-found checksums for downloaded files (optional)
      # (checksums are extracted from release's text body
      # based on following format `<sha256>  <filename>`)
      disableAutoChecksumValidation: true
      # specifies which archive to unpack for contents (optional)
      unpackArchive:
        path: release.tgz

    # copy contents from local directory (optional)
    directory:
      # local file system path relative to vendir.yml
      path: some-path

    # states that directory specified by above path
    # is managed by hand; nothing to do for vendir (optional)
    manual: {}

    # includes paths specify what should be included. by default
    # all paths are included (optional)
    includePaths:
    - cfroutesync/crds/**/*
    - install/ytt/networking/**/*

    # exclude paths are "placed" on top of include paths (optional)
    excludePaths: []

    # specifies paths to files that need to be includes for
    # legal reasons such as LICENSE file. Defaults to few 
    # LICENSE, NOTICE and COPYRIGHT variations (optional)
    legalPaths: []
```
