docker manifest inspect rhasspy/wyoming-vosk 
~~~
 docker manifest inspect rhasspy/wyoming-vosk 
{
   "schemaVersion": 2,
   "mediaType": "application/vnd.oci.image.index.v1+json",
   "manifests": [
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1050,
         "digest": "sha256:21404da367bb5bdcd5860b0e67f3c623a9fe617695582dcb4fba2f96a1adf83b",
         "platform": {
            "architecture": "amd64",
            "os": "linux"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1050,
         "digest": "sha256:3d7500a0d739c7064485e0e813de15f43d5bbdaa415b1a9130ae1ca7c7ac019e",
         "platform": {
            "architecture": "arm64",
            "os": "linux"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1050,
         "digest": "sha256:fc07bbc7c7aed0f0ee85d7de47ca0058a3a1172de44d8ea10e924eb8f8bd2256",
         "platform": {
            "architecture": "arm",
            "os": "linux",
            "variant": "v7"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 566,
         "digest": "sha256:8847cc24325b2b6f6a2da61c8a14054b586d7b06f2dd71c863626c30562fd098",
         "platform": {
            "architecture": "unknown",
            "os": "unknown"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 566,
         "digest": "sha256:b3c327a3f845dea908baaa5973418c4a0c320b7caba0da96057dc70def75349d",
         "platform": {
            "architecture": "unknown",
            "os": "unknown"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 566,
         "digest": "sha256:b4a7b34bfcdb7db9894a138372c0cfd5ecf49c1dde93a20c5e0d501c6b365114",
         "platform": {
            "architecture": "unknown",
            "os": "unknown"
         }
      }
   ]
}

~~~


~~~
docker manifest inspect  ghcr.io/mslycn/wyoming-vosk-standalone
manifest unknown
~~~