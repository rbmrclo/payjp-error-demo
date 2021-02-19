# Pay.JP Installation Problem Demo

#### `payjp`

```
$ docker build --no-cache -t payjp payjp
```

Error:

```
[+] Building 6.2s (6/6) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                         0.0s
 => => transferring dockerfile: 153B                                                                                                                                         0.0s
 => [internal] load .dockerignore                                                                                                                                            0.0s
 => => transferring context: 2B                                                                                                                                              0.0s
 => [internal] load metadata for docker.io/library/golang:1.15-alpine                                                                                                        0.0s
 => CACHED [1/3] FROM docker.io/library/golang:1.15-alpine                                                                                                                   0.0s
 => [2/3] RUN apk add --no-cache git                                                                                                                                         4.7s
 => ERROR [3/3] RUN go get github.com/payjp/payjp-go/v1                                                                                                                      1.5s
------
 > [3/3] RUN go get github.com/payjp/payjp-go/v1:
#6 0.700 go: downloading github.com/payjp/payjp-go v0.0.0-20201217084407-4e27e7ecbe9f
#6 1.425 go: found github.com/payjp/payjp-go/v1 in github.com/payjp/payjp-go v0.0.0-20201217084407-4e27e7ecbe9f
#6 1.439 go get: github.com/payjp/payjp-go@v0.0.0-20201217084407-4e27e7ecbe9f: parsing go.mod:
#6 1.439 	module declares its path as: v1
#6 1.439 	        but was required as: github.com/payjp/payjp-go
------
failed to solve with frontend dockerfile.v0: failed to build LLB: executor failed running [/bin/sh -c go get github.com/payjp/payjp-go/v1]: runc did not terminate sucessfully
```

#### `rbmrclo` (patched)

```
$ docker build --no-cache -t rbmrclo rbmrclo
```

Logs:
```
[+] Building 7.7s (8/8) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                         0.0s
 => => transferring dockerfile: 173B                                                                                                                                         0.0s
 => [internal] load .dockerignore                                                                                                                                            0.0s
 => => transferring context: 2B                                                                                                                                              0.0s
 => [internal] load metadata for docker.io/library/golang:1.15-alpine                                                                                                        0.0s
 => CACHED [1/4] FROM docker.io/library/golang:1.15-alpine                                                                                                                   0.0s
 => [2/4] RUN apk add --no-cache git                                                                                                                                         5.7s
 => [3/4] RUN go get github.com/rbmrclo/payjp-go/v1                                                                                                                          1.5s
 => [4/4] RUN echo "done"                                                                                                                                                    0.3s
 => exporting to image                                                                                                                                                       0.1s
 => => exporting layers                                                                                                                                                      0.1s
 => => writing image sha256:d9a982b484e598a91f8dba5731e38b51235becf1dd384a74e13695205edc9e83                                                                                 0.0s
 => => naming to docker.io/library/rbmrclo                                                                                                                                   0.0s
```

Patch:
```diff
diff --git a/go.mod b/go.mod
index 2e7b02d..8d69ff0 100644
--- a/go.mod
+++ b/go.mod
@@ -1,3 +1,3 @@
-module v1
+module github.com/payjp/payjp-go

 go 1.15
```
