# Deployment of NFTs through Volume

We will break this down into several steps, with an overview looking like:

1. Uploading each image/file to IPFS.
2. Creating a JSON file for each image/file with metadata about what was uploaded, and a pointer to the ipfs hash.
3. Upload of all the JSON files in one folder.

Don't worry if you don't know how to do these things - we will take you through it and do the heavy lifting for you :sweat_smile:.

## 1. Uploading each image/file to IPFS

This means you will upload each image or file in your collection to IPFS first. You can use any IPFS gateway to deploy it. The important thing is making sure to store each image hash. This is the hash used to resolve to the image/file, and the one we will use in the JSON file in step 2.

Here is a list of of public gateways:
https://ipfs.github.io/public-gateway-checker/

## 2. Creating JSON files

We will now create the JSON files for each image/file you deployed in the previous step. If you have a big collection, chances are that you already have a JSON file for each file in your collection.

Please use iterating numbers as names for your json files - so if you have 5 files:

```
1.json
2.json
3.json
4.json
5.json
```

The important thing is to have a JSON schema like this:

```
{
    "title": "Asset Metadata",
    "type": "object",
    "properties": {
        "name": {
            "type": "string",
            "description": "Identifies the asset to which this NFT represents"
        },
        "description": {
            "type": "string",
            "description": "Describes the asset to which this NFT represents"
        },
        "image": {
            "type": "string",
            "description": "A URI pointing to a resource with mime type image/* representing the asset to which this NFT represents. Consider making any images at a width between 320 and 1080 pixels and aspect ratio between 1.91:1 and 4:5 inclusive."
        }
    }
}
// Snippet from https://eips.ethereum.org/EIPS/eip-721#implementations
```

It doesn't have to be EXACTLY like this, but the idea is that you describe the varying properties of your NFT. For instance if I have a collection where each image consists of a type of cat with some sort of hat on, my JSON schema might look something like this: 
```
{
    "title": "Kitty 1",
    "type": "object",
    "properties": {
        "name": {
            "type": "string",
            "description": "First Kitty"
        },
        "breed": {
            "type": "string",
            "description": "Persian"
        },
        "hat": {
            "type": "string",
            "description": "Top Hat"
        },
        "image": {
            "type": "string",
            "description": "ipfs://{KITTY_HASH}"
        }
    }
}
```

## 3. Uploading all JSON files

Now that we have created the metadata and linked the image, we are ready to deploy the folder.

You are again welcome to use any IPFS gateway of your choice, just be sure to store the CID hash of your folder as you will need it to find your files.

## Final thoughts

If you are having trouble understanding the deployment and would like to launch a collection through the `Volume INO` please contact the volume team [here](mailto:contact@volume.quest) for assistance.

Resources:

* [EIP721 standard](https://eips.ethereum.org/EIPS/eip-721)