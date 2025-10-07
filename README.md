# chutvrc dialog

[![License: MPL 2.0](https://img.shields.io/badge/License-MPL%202.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)

The WebRTC-side code for [chutvrc](https://github.com/pf-hubs/chutvrc-hubs), forked from [dialog](https://github.com/mozilla/dialog), to provide mediasoup based WebRTC SFU.

## chutvrc features

Some notable features for chutvrc are,

- Full-body avatar (ReadyPlayerMe, VRoid)
- BitECS implementation
- Alternative WebRTC SFU (selection for Third-Pary WebRTC)
- Synchronizing avatar transform with WebRTC DataChannel

For more details, please see the [client-side code for chutvr](https://github.com/pf-hubs/chutvrc-hubs).

## Funding and Sponsor

<div align="center">
    <img src=".github/media/vrcenter-logo.png" width="320">
    <img src=".github/media/change-logo.png" width="320">
</div>

- chutvrc is sponsored and developed for [CHANGE Project](https://change.kawasaki-net.ne.jp/en/), by a research team at the [Virtual Reality Educational Research Center](https://vr.u-tokyo.ac.jp/), The University of Tokyo.
- You can support this development through the GitHub Sponsor button which is linked to the [UTokyo Foundation](https://utf.u-tokyo.ac.jp/en).
- If you want to support this project only, please write in the donation purpose "For Virtual Reality Educational Research Center, chutvrc related research/educational purpose."
  - Please be aware that 30% of the amount of donation will be used by the university administration office even if you write the donation purpose.

---

Below is the original README for Mozilla dialog, which most information are also useful for chutvrc.

It will be updated to migration information considering the current status of Mozilla Hubs, which is planned to shutdown at the end of May 2024.

---

Mediasoup based WebRTC SFU for Mozilla Hubs.

## Development
1. Clone repo
2. In root project folder, `npm ci` (this may take a while).
3. Create a folder in the root project folder called `certs` if needed (see steps 4 & 5).
4. Add the ssl cert and key to the `certs` folder as `fullchain.pem` and `privkey.pem`, or set the path to these in your shell via `HTTPS_CERT_FULLCHAIN` and `HTTPS_CERT_PRIVKEY` respectively. You can provide these certs yourself or use the ones available in https://github.com/mozilla/reticulum/tree/master/priv (`dev-ssl.cert` and `dev-ssl.key`).

5. Add the reticulum permissions public key to the `certs` folder as `perms.pub.pem`, or set the path to the file in your shell via `AUTH_KEY`.

  * If using one of the public keys from hubs-ops (located in https://github.com/mozilla/hubs-ops/tree/master/ansible/roles/janus/files), you will need to convert it to standard pem format.    
    * e.g. for use with dev.reticulum.io:  `openssl rsa -in perms.pub.der.dev -inform DER -RSAPublicKey_in -out perms.pub.pem`

6. Start dialog with `MEDIASOUP_LISTEN_IP=XXX.XXX.XXX.XXX MEDIASOUP_ANNOUNCED_IP=XXX.XXX.XXX.XXX npm start` where `XXX.XXX.XXX.XXX` is the local IP address of the machine running the server. (In the case of a VM, this should be the internal IP address of the VM).
  * If you choose to set the paths for `HTTPS_CERT_FULLCHAIN`, `HTTPS_CERT_PRIVKEY` and/or `AUTH_KEY` you may also define them inline here as well. e.g. 
  ```
  HTTPS_CERT_FULLCHAIN=/path/to/cert.file HTTPS_CERT_PRIVKEY=/path/to/key.file AUTH_KEY=/path/to/auth.key MEDIASOUP_LISTEN_IP=XXX.XXX.XXX.XXX MEDIASOUP_ANNOUNCED_IP=XXX.XXX.XXX.XXX npm start
  ```
     
7. Navigate to https://localhost:4443/ in your browser, and accept the self-signed cert.

8. You may now point Hubs/Reticulum to use `localhost:4443` as the WebRTC host/port.`

See `config.js` for all available configuration options.
