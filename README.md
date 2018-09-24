# Mined For Change

This repository exists to verify the [Mined For Change website](https://minedforchange.org).

Mined For Change is a charity that exists to fill in the gaps of donation. People who may not have lots to give or wish for another way to give besides credit card payments can simply open the site and start mining cryptocurrency for charity. It may not be a lot individually but together with thousands of other equally generous people, we can raise impressive amounts of money for the [Against Malaria Foundation](#against-malaria-foundation).

Best of all, the entire process is verifiable. That is, anyone can verify that the funds they (and others) generate are actually being given to the right place. While the movement begins to grow, it is necessary for the funds to be held by someone. Mined For Change allows anyone to see the funds received and will publish all transactions to the AMF when a certain sum has built up. Hopefully one day we will be able to pay the mosquitto net manufacturers directly, eliminating all middlemen, and maximising each donation.

For more on Mined for Change and how we embody effective altruism, please [see our blog](https://medium.com/@minedforchange).

## Folders

This folder contains the following files:

MinedForChange
├── MinedForChange-Website/
├── README.md
├── sha256sum.txt
└── sha256sum.txt.asc


## Verification

To verify the website is as it was uploaded follow these steps:

### Download the website from your browser.

#### Linux or Mac

This can be done easily using `wget`:

```
wget -r --no-parent https://minedforchange.org
```

The two mining scripts are missing since they are loaded asynchronously when someone starts mining. To get them:

```
cd minedforchange.org/js
wget https://minedforchange.org/js/worker.js https://minedforchange.org/js/cryptonote.js
```


The files should be saved automatically like this:

```
└── minedforchange.org
    ├── apple-touch-icon.png
    ├── css
    │   └── style.css
    ├── favicon-16x16.png
    ├── favicon-32x32.png
    ├── img
    │   ├── jared.jpg
    │   ├── mfc-logo-transparent-light.png
    │   ├── mfc-logo-transparent.png
    │   ├── mfcmodal.jpg
    │   ├── mosnet2.jpg
    │   └── tom.jpg
    ├── index.html
    ├── js
    │   ├── cryptonote.js
    │   ├── m4c.js
    │   ├── main.js
    │   ├── NoSleep.min.js
    │   ├── startMiner.js
    │   └── worker.js
    ├── safari-pinned-tab.svg
    └── site.webmanifest
```

There are additionally some image files that are missing which you can save in a similar manner. From the root directory of the saved website:

```
wget https://minedforchange.org/mstile-150x150.png https://minedforchange.org/favicon.ico https://minedforchange.org/error.html https://minedforchange.org/apple-touch-icon.png https://minedforchange.org/browserconfig.xml

cd img
wget https://minedforchange.org/img/android-chrome-192x192.png https://minedforchange.org/img/android-chrome-512x512.png https://minedforchange.org/img/og-image.jpg
```

#### Windows

If you don't want to use the above options for Linux or Mac, or you are using a Windows machine, you can use the [HTTrack tool](http://www.httrack.com/) to save the files.


### Clone or Download this Repository

Move the `sha256sum.txt` file from this repository into the folder with the website files.

This can be done by cloning the repo or manually by clicking on the file above, clicking `Raw` then press CTRL+S and save the file in the same place as the other documents.


### Verify the Checksums

#### Mac or Linux

1. On Mac or Linux, use the `sha256sum` command to compare the checksums of the files:
```bash
sha256sum --check sha256sum.txt
```

Which should result in:
```
sha256sum --check sha256sum.txt
./apple-touch-icon.png: OK
./browserconfig.xml: OK
./error.html: OK
./favicon-16x16.png: OK
./favicon-32x32.png: OK
./favicon.ico: OK
./index.html: OK
./mstile-150x150.png: OK
./safari-pinned-tab.svg: OK
./site.webmanifest: OK
./css/style.css: OK
./img/android-chrome-192x192.png: OK
./img/android-chrome-512x512.png: OK
./img/jared.jpg: OK
./img/mfc-logo-transparent-light.png: OK
./img/mfc-logo-transparent.png: OK
./img/mfcmodal.jpg: OK
./img/mosnet2.jpg: OK
./img/og-image.jpg: OK
./img/tom.jpg: OK
./js/cryptonote.js: OK
./js/m4c.js: OK
./js/main.js: OK
./js/NoSleep.min.js: OK
./js/startMiner.js: OK
./js/worker.js: OK
```

All the files that are downloaded should be marked as OK and are thus the same as they were uploaded. If there are files that are not ok, first check if they have all been downloaded otherwise go back to step 1.

#### Windows

On Windows, the process varies depending on your version. The simplest solution is to use a simple third party program such as [HashCheck](http://code.kliu.org/hashcheck/).

If you have Windows >= 7 you can use the following command from the command line to generate the hashes of each file:

```bash
certUtil -hashfile ./* SHA256
```

The hashes of each file that is saved should be marked as OK and are thus the same as they were uploaded. If there are files that are not ok, first check if they have all been downloaded otherwise go back to step 1.



### Verify Hashfile with PGP

To verify the integrity of the hashfile, you can use the developer's PGP signature (that's me). First download the `sha256sum.txt.asc` file from this repo and place it in the same folder as the `sha256sum.txt` file.

Then download the developer's PGP key from keyservers:

```
gpg --recv-keys 54DC 84E3 7FDD 0DFE BB8D 39B7 447E 1B93 6DA3 9F99
```


On Mac or Linux, to verify the gpg signature of the `sha256sum.txt` file and thus prooving its originality from Mined For Change, type the following:

```bash
gpg --verify sha256sum.txt.asc sha256sum.txt
```

This should result in something like the following:
```
gpg: Signature made Mon 24 Sep 2018 22:00:23 SAST using RSA key ID 6DA39F99
gpg: Good signature from "Thomas Tumiel (Creating GPG key for Github.) <ttumiel@gmail.com>"
```



On Windows, third party software is needed again. Some useful tools are [Gpg4win](https://www.gpg4win.org/) or [GPGShell](http://www.tech-faq.com/gnupg-shell.html)


## About the Verification Process

### Checksums

This is essentially a cryptographic technique that gives a unique fingerprint to any document. By looking at the fingerprint and seeing if it's the same, we can see that the file has not been altered.

For more explanation on checksums, see the following links:

https://www.howtogeek.com/363735/what-is-a-checksum-and-why-should-you-care/

https://en.wikipedia.org/wiki/Checksum



### PGP Signatures

A PGP signature is an encryption method that proves a message was signed by a specific person. By verifying that I signed the `sha256sum.txt` hashfile, you can be sure that the checksums provided are the ones that I created and not a third party.

For more about PGP signatures, see the following links:

https://www.alienvault.com/blogs/security-essentials/explain-pgp-encryption-an-operational-introduction

https://en.wikipedia.org/wiki/Pretty_Good_Privacy

https://xkcd.com/1181/

### The Mining Script

Anyone can inspect the open source mining script, found in the `m4c.js`, `worker.js` and `cryptonote.js` files. The public address below enables anyone to view the funds that have been generated. As a result of the choice of currency to mine (Monero) an additional private viewkey is required to view the funds of an account.

The public details of the Monero Wallet are as follows:

**Public Address:**
```
489WzMtWjeKSaDCuNdxJSEftaLxDPeUUQHdYWMVE54RJgMHVLmtzp3p5q9ziYf2kwTXceD5pxzm574MmQpvpEPvbDWuvhU8
```


**Private Viewkey:**
```
dd5ee3430634511b81c5248957192930ccea428c2f4db78a8df6e08caa65590d
```


Using these 2 pieces of information, anyone can see the funds coming into this address. This will occur periodically when the pool pays out to the address and will be published as time goes on.

For more information on the way Monero encrypts its data and how the private viewkey works, see here:

https://monero.stackexchange.com/questions/954/how-to-use-the-view-key-to-see-amount-sent-to-cold-storage

https://steemit.com/monero/@luigi1111/understanding-monero-cryptography-privacy-introduction

https://getmonero.org/


### Sub-Resource Integrity

You will also notice that all files called from the `index.html` file reference the particular javascript and css files with integrity checks. This means that the only file that is really necessary to check is the `index.html` file as it already contains the fingerprints of all the other files.



## Against Malaria Foundation

We support the [Against Malaria Foundation](https://www.againstmalaria.com) - a high-impact charity. The AMF has a well researched and independently verified history of maximising the number of lives saved per dollar donated and thus they were chosen as the charity of choice at Mined For Change. In conversation with the AMF, it was decided, since they are a large organisation and aim to minimise administrative difficulty, that a donations page on with the AMF would be created to cross-verify Mined For Change.

[See our Against Malaria Foundation donations page.](https://www.againstmalaria.com/MinedForChange)

Simple click the `button` to view the Monero wallet keys.


## A Small Note on Browsers

For reasons beyond me, Chrome downloads websites with all `.js` and `.css` files as `.min.js` and `.min.css` whereas Firefox saves them as purely `.js` and `.css`. This happened both when the files are served as plain `.js` and `.css` or the minified extension `.min.js` and `.min.css` regardless of content. Furthermore, this does not place files in folders, breaking the naming pattern again.

For these reasons it is not recommended to save the page using CTRL+s in your browser but it is possible if you manually rename the files in the `sha256sum.txt` file to whatever they are saved as.



## Questions or Comments

Please get in touch with us:

Thomas (@Tom2718) - thomas (at) minedforchange (dot) org

Jared (@jarry401) - jared (at) minedforchange (dot) org
