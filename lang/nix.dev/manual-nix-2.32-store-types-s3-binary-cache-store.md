---
url: https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store
title: S3 Binary Cache Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# S3 Binary Cache Store - Nix 2.32.2 Reference Manual

# [S3 Binary Cache Store](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#s3-binary-cache-store)

**Store URL format**: `s3://`*bucket-name*

This store allows reading and writing a binary cache stored in an AWS S3 (or S3-compatible service) bucket.
This store shares many idioms with the [HTTP Binary Cache Store](https://nix.dev/manual/nix/2.32/store/types/http-binary-cache-store).

For AWS S3, the binary cache URL for a bucket named `example-nix-cache` will be exactly <s3://example-nix-cache>.
For S3 compatible binary caches, consult that cache's documentation.

### [Anonymous reads to your S3-compatible binary cache](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#anonymous-reads-to-your-s3-compatible-binary-cache)

> If your binary cache is publicly accessible and does not require authentication,
> it is simplest to use the [HTTP Binary Cache Store] rather than S3 Binary Cache Store with
> <https://example-nix-cache.s3.amazonaws.com> instead of <s3://example-nix-cache>.

Your bucket will need a
[bucket policy](https://docs.aws.amazon.com/AmazonS3/v1/userguide/bucket-policies.html)
like the following to be accessible:

```
{
    "Id": "DirectReads",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowDirectReads",
            "Action": [
                "s3:GetObject",
                "s3:GetBucketLocation"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:s3:::example-nix-cache",
                "arn:aws:s3:::example-nix-cache/*"
            ],
            "Principal": "*"
        }
    ]
}
```

### [Authentication](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#authentication)

Nix will use the
[default credential provider chain](https://docs.aws.amazon.com/sdk-for-cpp/v1/developer-guide/credentials.html)
for authenticating requests to Amazon S3.

Note that this means Nix will read environment variables and files with different idioms than with Nix's own settings, as implemented by the AWS SDK.
Consult the documentation linked above for further details.

### [Authenticated reads to your S3 binary cache](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#authenticated-reads-to-your-s3-binary-cache)

Your bucket will need a bucket policy allowing the desired users to perform the `s3:GetObject` and `s3:GetBucketLocation` action on all objects in the bucket.
The [anonymous policy given above](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#anonymous-reads-to-your-s3-compatible-binary-cache) can be updated to have a restricted `Principal` to support this.

### [Authenticated writes to your S3-compatible binary cache](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#authenticated-writes-to-your-s3-compatible-binary-cache)

Your account will need an IAM policy to support uploading to the bucket:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "UploadToCache",
      "Effect": "Allow",
      "Action": [
        "s3:AbortMultipartUpload",
        "s3:GetBucketLocation",
        "s3:GetObject",
        "s3:ListBucket",
        "s3:ListBucketMultipartUploads",
        "s3:ListMultipartUploadParts",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::example-nix-cache",
        "arn:aws:s3:::example-nix-cache/*"
      ]
    }
  ]
}
```

### [Examples](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#examples)

With bucket policies and authentication set up as described above, uploading works via [`nix copy`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy) (experimental).

* To upload with a specific credential profile for Amazon S3:

  ```
  $ nix copy nixpkgs.hello \
    --to 's3://example-nix-cache?profile=cache-upload&region=eu-west-2'
  ```
* To upload to an S3-compatible binary cache:

  ```
  $ nix copy nixpkgs.hello --to \
    's3://example-nix-cache?profile=cache-upload&scheme=https&endpoint=minio.example.com'
  ```

## [Settings](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#settings)

* [`buffer-size`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-buffer-size)

  Size (in bytes) of each part in multi-part uploads.

  **Default:** `5242880`
* [`compression`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-compression)

  NAR compression method (`xz`, `bzip2`, `gzip`, `zstd`, or `none`).

  **Default:** `xz`
* [`compression-level`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-compression-level)

  The *preset level* to be used when compressing NARs.
  The meaning and accepted values depend on the compression method selected.
  `-1` specifies that the default compression level should be used.

  **Default:** `-1`
* [`endpoint`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-endpoint)

  The URL of the endpoint of an S3-compatible service such as MinIO.
  Do not specify this setting if you're using Amazon S3.

  > **Note**
  >
  > This endpoint must support HTTPS and uses path-based
  > addressing instead of virtual host based addressing.

  **Default:** *empty*
* [`index-debug-info`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-index-debug-info)

  Whether to index DWARF debug info files by build ID. This allows [`dwarffs`](https://github.com/edolstra/dwarffs) to
  fetch debug info on demand

  **Default:** `false`
* [`local-nar-cache`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-local-nar-cache)

  Path to a local cache of NARs fetched from this binary cache, used by commands such as `nix store cat`.

  **Default:** *empty*
* [`log-compression`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-log-compression)

  Compression method for `log/*` files. It is recommended to
  use a compression method supported by most web browsers
  (e.g. `brotli`).

  **Default:** *empty*
* [`ls-compression`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-ls-compression)

  Compression method for `.ls` files.

  **Default:** *empty*
* [`multipart-upload`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-multipart-upload)

  Whether to use multi-part uploads.

  **Default:** `false`
* [`narinfo-compression`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-narinfo-compression)

  Compression method for `.narinfo` files.

  **Default:** *empty*
* [`parallel-compression`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-parallel-compression)

  Enable multi-threaded compression of NARs. This is currently only available for `xz` and `zstd`.

  **Default:** `false`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`profile`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-profile)

  The name of the AWS configuration profile to use. By default
  Nix uses the `default` profile.

  **Default:** *empty*
* [`region`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-region)

  The region of the S3 bucket. If your bucket is not in
  `us-east-1`, you should always explicitly specify the region
  parameter.

  **Default:** `us-east-1`
* [`scheme`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-scheme)

  The scheme used for S3 requests, `https` (default) or `http`. This
  option allows you to disable HTTPS for binary caches which don't
  support it.

  > **Note**
  >
  > HTTPS should be used if the cache might contain sensitive
  > information.

  **Default:** *empty*
* [`secret-key`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-secret-key)

  Path to the secret key used to sign the binary cache.

  **Default:** *empty*
* [`secret-keys`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-secret-keys)

  List of comma-separated paths to the secret keys used to sign the binary cache.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`
* [`write-nar-listing`](https://nix.dev/manual/nix/2.32/store/types/s3-binary-cache-store#store-s3-binary-cache-store-write-nar-listing)

  Whether to write a JSON file that lists the files in each NAR.

  **Default:** `false`