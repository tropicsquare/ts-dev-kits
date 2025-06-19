# TROPIC01 USB Dev Kit
<img src="https://github.com/tropicsquare/ts13-dev-kit/blob/TS1302/img/angle.png" alt="TROPIC01 next to STM32U5 microcontroller" width="300" align="right">
TROPIC01 objective is trustless, auditable security. 
The TROPIC01's unique design, coupled with its flexible firmware, puts you in complete control. It's built for raw data transfer, empowering your host application to define and manage all key handling and security policies. You can tailor TROPIC01 to fit your exact security architecture and trust models. For a comprehensive exploration of how TROPIC01 can empower your projects, we invite you to connect directly with our business representatives.

# Use Cases

USB dev kit is a platform enabling TROPIC01 evaluation with systems where SPI is not available. Here's a glimpse into the potential of the TROPIC01 USB Dev Kit:

* **FIDO2/WebAuthn Authentication**  
Improve user identity verification by leveraging robust cryptographic keys and eliminating reliance on vulnerable passwords.

* **SmartCard/PIV/OpenPGP Token**  
Seamlessly emulate a high-security smart card for critical operations like secure signing, robust encryption, and login processes (e.g., SSH, GPG).

* **Digital Signature and Timestamping**  
Confidently secure your documents, data, and transactions with verified digital signatures and precise timestamping, whether online or offline.

# Quickguide

This guide provides a first look at the TROPIC01 USB Dev Kit's core capabilities, offering a launchpad for your secure development. We've designed TROPIC01 to be a playground for secure development. This guide is just the beginning; we encourage you to experiment, customize, and push the boundaries of what's possible. Our comprehensive TROPIC01 Documentation is packed with examples and resources to help you build unique security solutions.

### Your development kit contains:

* **TROPIC01 USB Dongle** - Your dedicated tool for secure development.

* **This instruction guide** - Your immediate document to getting started.

### Prerequisites

* Any **Linux-based Operating System**

  * GIT

  * CMAKE

  * GCC

* USB-C port

### Deployment

Follow these steps to establish communication with your USB dongle:

1. Before plugging your USB dongle into the USB port, execute the following command:

```
sudo dmesg -w
```

2. Plug your USB dongle in. The device enumerates in your system.
```
[525111.353351] usb 3-1: new full-speed USB device number 14 using xhci_hcd
[525111.751097] usb 3-1: New USB device found, idVendor=0483, idProduct=5740, bcdDevice= 2.00
[525111.751105] usb 3-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[525111.751107] usb 3-1: Product: SPI interface
[525111.751108] usb 3-1: Manufacturer: TropicSquare
[525111.751109] usb 3-1: SerialNumber: 1e2500773388
[525111.753256] cdc_acm 3-1:1.0: ttyACM0: USB ACM device
``` 

> ttyACM0: USB ACM device, this means that USB dongle is enumerated as `/dev/ttyACM0`.

3. To obtain tools and documentation, run:  
```
git clone https://github.com/tropicsquare/libtropic-util.git
```
5. Move into libtropic-util directory  
```
cd libtropic-util/
```
7. Update modules  
```
git submodule update --init --recursive
```
9. To compile, run:  
```
mkdir build
cd build
cmake -DUSB_DONGLE=1 ..
make
```
7. Execute from bash and use for the direct access to TROPIC01 features. Refer to the [libtropic-util](https://github.com/tropicsquare/libtropic-util?tab=readme-ov-file#usb-dongle-with-tropic01-chip) document for the expected output. 
```
./lt-util

```
### Example of use

In this example, we want to ensure that the system works correctly. Test dependencies are described in **README.md**.

1. Go into test folder.

2. Run test command:

```
./run_tests_usb.sh
```

* Red LED will blink multiple times on USB dongle. 

* Tests takes approximately 10 seconds. 

* Similar output to the one below will be visible in your terminal:

```
[COMMAND] RNG test expected fails with invalid length:
  Status:  1
  Status:  1
  Status:  1
[COMMAND] Get 32 random bytes and save as message:
  Status:  0
[COMMAND] Erase slot 0: 
  Status:  0
[COMMAND] Generate EdDSA keypair there: 
  Status:  0
[COMMAND] Get public key
  Status:  0
[COMMAND] Sign message 5 times
  Status:  0
  Status:  0
  Status:  0
  Status:  0
  Status:  0

[INFO] Verify five signatures with python cryptography library
Message: 1edbf3b37df401e7718797bcfd842816a793f705113899450a598e03c2b28097
Public key: 8ee335c06109b907d74005571a2e766877a4ae142c4d6a8c60e488e85707bd2d
Signature: 70accba9fe6d4d82e94ea01ead3d8fc7ac96f0d87e666e60f1c2c2be1b5c9e1d22cecd8a9a32632b06b4577d1b6251de0e59a281784a61012653da7b05ee4302
Signature verification SUCCEEDED
Message: 1edbf3b37df401e7718797bcfd842816a793f705113899450a598e03c2b28097
Public key: 8ee335c06109b907d74005571a2e766877a4ae142c4d6a8c60e488e85707bd2d
Signature: 156b793cf7300b619c9e1fe4e3428f5118e614f326a2e0d7c6c42730f129b9920e0a00fc691da0c40970de9a844ea4cb38fe74e2c5463e301c5e0249fc981b0a
Signature verification SUCCEEDED
Message: 1edbf3b37df401e7718797bcfd842816a793f705113899450a598e03c2b28097
Public key: 8ee335c06109b907d74005571a2e766877a4ae142c4d6a8c60e488e85707bd2d
Signature: 4b60b1e50f4268d1b37cadf2645137bb0bcc443c92021f66fce9253dfea0be3ead540a10c5b509a6969ba4cfda7b59d94e320b9d665fb93bc0154490770f0d0a
Signature verification SUCCEEDED
Message: 1edbf3b37df401e7718797bcfd842816a793f705113899450a598e03c2b28097
Public key: 8ee335c06109b907d74005571a2e766877a4ae142c4d6a8c60e488e85707bd2d
Signature: d030385831f8e0e95931c5ce09cc31828dbbff08cc0f0364727ea6fc7fa54c0f261efca70525147864e223027806abfd24be8c38cf5a5ff924ca56fde4bb6104
Signature verification SUCCEEDED
Message: 1edbf3b37df401e7718797bcfd842816a793f705113899450a598e03c2b28097
Public key: 8ee335c06109b907d74005571a2e766877a4ae142c4d6a8c60e488e85707bd2d
Signature: 9a768e4fd4a5acce0fff16761ed46566418b88e9cc7a4e94e737bce22c587de5a8a7fbb6edb635cd5e24918bbedd8f3257da01f21617dd9a98388dcaac0ab807
Signature verification SUCCEEDED
/home/ppolach/Desktop/libtropic-util/test
```
## Reference Links

* [Firmware repository](https://github.com/tropicsquare/ts13-usb-dev-kit-fw/tree/ts1302)

* [Hardware repository](https://github.com/tropicsquare/ts13-dev-kit/tree/TS1302)

* [Application repository: libtropic-util](https://github.com/tropicsquare/libtropic-util)

## Disclaimer

* We are not a company manufacturing USB devices as end-user products.
* The TS1302 USB development kit featuring the Tropic Square TR01 uses STM32U5 microcontroller. 
* For our license disclaimer, please follow this [link](https://github.com/tropicsquare/libtropic/blob/master/LICENSE.md).
