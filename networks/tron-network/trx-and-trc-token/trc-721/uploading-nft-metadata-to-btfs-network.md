# Uploading NFT Metadata to BTFS Network

BitTorrent File System \(BTFS\) is a next-generation file-sharing protocol utilizing the TRON network and the BitTorrent ecosystem.

Metadata is the detailed information of the NFT token. It is stored off the chain. Generally, the issuance of an NFT token will specify a URI path that points to the Metadata data of the token.

### 1 Install BTFS

Refer to [BTFS Installation Instructions](https://docs.btfs.io/docs/btfs-demo).

### 2 Deposit BTT

Uploading files to the BTFS network requires BTT as the payment method.

The current storage price is 0.0037 BTT/Mb/month. For the uploader, redundant information will be added to the uploaded file and split into 30 copies. Any ten copies can be restored into a complete file so that each file will be uploaded three times the original file size. That is, for the uploader, the price is 3\*0.0037 BTT/Mb/month\(about $0.000038/Mb/month, calculated with the current price\).

While using `btfs init` to initialize the local node, the command will generate a TRON wallet account associated with the node. You can check the TRON address corresponding to the wallet through `btfs id`.

![](https://files.readme.io/bef9ccd-641616987616_.pic_hd.jpg)

![](https://files.readme.io/bef9ccd-641616987616_.pic_hd.jpg)

First, you need to recharge some BTT to the node's TRON account and then transfer the BTT of the TRON account to the accounting system of the BTFS network.

#### Set a Password

Run the following command to set a password for the node wallet:Shell

```text
btfs wallet password   **********
```

#### Transfer BTT to BTFS network accounting system

Running the following command will transfer the BTT of the local BTFS node account to the accounting system of the BTFS network. The minimum transfer amount is 10 BTT, and the BTT unit specified in the following command is μBTT \(1/1000000 of BTT\):Shell

```text
btfs wallet deposit -p *********  10000000
```

### 3 Upload the File

#### Step 1: Prepare a picture and name the picture coral.jpeg

![](https://files.readme.io/e53617d-611616987482_.pic_hd.jpg)

![](https://files.readme.io/e53617d-611616987482_.pic_hd.jpg)

#### Step 2: Use Reed-Solomon encoding to add pictures to the local node

Shell

```text
btfs add --chunker=reed-solomon coral.jpeg
```

![](https://files.readme.io/a16e85b-621616987528_.pic_hd.jpg)

![](https://files.readme.io/a16e85b-621616987528_.pic_hd.jpg)

The `QmUK9nwtLEiHBJ48HAZHNmSQ53U6ADbRhATxs2tomadwKw` in the picture is the hash value of the file.

#### Step 3: Upload files to the BTFS network through this hash value:

Shell

```text
btfs storage upload QmUK9nwtLEiHBJ48HAZHNmSQ53U6ADbRhATxs2tomadwKw
```

![](https://files.readme.io/f19d5b8-631616987592_.pic_hd.jpg)

![](https://files.readme.io/f19d5b8-631616987592_.pic_hd.jpg)

When you see "File storage successful" in the window of `btfs daemon`, it means the upload is successful

![](https://files.readme.io/1a87623-641616987616_.pic_hd.jpg)

![](https://files.readme.io/1a87623-641616987616_.pic_hd.jpg)

#### Step 4: Verify that the picture can be downloaded

Open the following link of the picture in the browser, you can see the picture indicating that the picture can be downloaded successfully:

[https://gateway.btfs.io/btfs/QmUK9nwtLEiHBJ48HAZHNmSQ53U6ADbRhATxs2tomadwKw](https://gateway.btfs.io/btfs/QmUK9nwtLEiHBJ48HAZHNmSQ53U6ADbRhATxs2tomadwKw)

![](https://files.readme.io/89b6fe0-651616987651_.pic_hd.jpg)

![](https://files.readme.io/89b6fe0-651616987651_.pic_hd.jpg)

### 4 Construct the NFT metadata file

You can use the image link above to construct metadata for NFT.

Create a JSON file according to the metadata example in the TRC-721 document and name it coral.json, and replace the description value in the image field with the BTFS download link of the image above, as shown in the figure:

![](https://files.readme.io/fd99909-661616987692_.pic.jpg)

![](https://files.readme.io/fd99909-661616987692_.pic.jpg)

Run the btfs command to upload coral.json:

![](https://files.readme.io/43483fc-671616987719_.pic_hd.jpg)

![](https://files.readme.io/43483fc-671616987719_.pic_hd.jpg)

Open the URI of the metadata file in the browser:  
[https://gateway.btfs.io/btfs/QmWq4cp588QD8tzrSxvPs2bGikDdKyA35BT3iysBcP1jFD](https://gateway.btfs.io/btfs/QmWq4cp588QD8tzrSxvPs2bGikDdKyA35BT3iysBcP1jFD)  


![](https://files.readme.io/6b62b0f-681616987739_.pic.jpg)

![](https://files.readme.io/6b62b0f-681616987739_.pic.jpg)

